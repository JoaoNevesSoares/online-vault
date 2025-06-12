
```GLSL
//SÓ UM CIRCULO FEIO
void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    
    //desloca sistema coordenadas para meio da tela
    uv -= .5;
    
    // redimensiona os pontos para tamanho pixels da tela
    uv.x *= iResolution.x / iResolution.y;
    
    float radius = .3;
    float dist_vector = length(uv);
    float color_unit = 0.;
    if(dist_vector < radius){
        color_unit += 1.0;
     }
    vec3 color = vec3(color_unit);

    // Output to screen
    fragColor = vec4(color,1.0);
}
```

```GLSL
//EMOJI DE CARINHA FELIZ
float Circulo(vec2 uv, vec2 origin,float radius){

    float c = 0.;
    float dist = length(uv-origin);
    if(dist < radius){
        c+=1.0;
    }
    return c;
}

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    
    //desloca sistema coordenadas para meio da tela
    uv -= .5;
    
    // redimensiona os pontos para tamanho pixels da tela
    uv.x *= iResolution.x / iResolution.y;
    
    float radius = .3;
    float dist_vector = length(uv);
    float mask = Circulo(uv,vec2(.0),radius);
    
    //os olhinhos
    mask -= Circulo(uv,vec2(0.1,0.1),0.03);
    mask -= Circulo(uv,vec2(-0.1,0.1),0.03);
    
    // a boquinha
    float mouth = Circulo(uv,vec2(0.,-0.05),0.1) - Circulo(uv,vec2(0.),0.1);
    mask -= mouth;
    vec3 color = vec3(1.,1.,0.)*mask;
    // Output to screen
    fragColor = vec4(color,1.0);
}
```

```GLSL
float Circulo(vec2 uv, vec2 origin,float radius){

    float c = 0.;
    float dist = length(uv-origin);
    if(dist < radius){
        c+= smoothstep(radius,radius-0.01,dist);
    }
    return c;
}

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    // Normalized pixel coordinates (from 0 to 1)
    vec2 uv = fragCoord/iResolution.xy;
    
    //desloca sistema coordenadas para meio da tela
    uv -= .5;
    
    // redimensiona os pontos para tamanho pixels da tela
    uv.x *= iResolution.x / iResolution.y;
    
    float radius = .3;
    float dist_vector = length(uv);
    float cat_ad = cos(.05) * radius -0.1;
    float cat_op = sin(.05) * radius;
    float r_mask = Circulo(uv,vec2(0.,0.2),radius);
    float b_mask = Circulo(uv,vec2(-cat_ad,-cat_op),radius);
    float g_mask = Circulo(uv,vec2(cat_ad,-cat_op),radius);
    vec3 color = vec3(r_mask*1.0,1.0*g_mask,b_mask*1.0);
    // Output to screen
    fragColor = vec4(color,1.0);
}
```


# CODIGOS FINAIS

```GLSL

// "ShaderToy Tutorial - Ray Marching Primitives" 
// by Martijn Steinrucken aka BigWings/CountFrolic - 2019
// License Creative Commons Attribution-NonCommercial-ShareAlike 3.0 Unported License.
//
// This shader is part of a tutorial on YouTube
// https://youtu.be/Ff0jJyyiVyw

#define MAX_STEPS 100
#define MAX_DIST 100.
#define SURF_DIST .0001

mat2 Rot(float a) {
    float s = sin(a);
    float c = cos(a);
    return mat2(c, -s, s, c);
}

float smin( float a, float b, float k ) {
    float h = clamp( 0.5+0.5*(b-a)/k, 0., 1. );
    return mix( b, a, h ) - k*h*(1.0-h);
}

float sdSphere( vec3 p, float s )
{
  return length(p)-s;
}
float SdSphere( in vec3 p, in vec4 s )
{
    return length(p-s.xyz) - s.w;
}
float sdCapsule(vec3 p, vec3 a, vec3 b, float r) {
	vec3 ab = b-a;
    vec3 ap = p-a;
    
    float t = dot(ab, ap) / dot(ab, ab);
    t = clamp(t, 0., 1.);
    
    vec3 c = a + t*ab;
    
    return length(p-c)-r;
}

float sdCylinder(vec3 p, vec3 a, vec3 b, float r) {
	vec3 ab = b-a;
    vec3 ap = p-a;
    
    float t = dot(ab, ap) / dot(ab, ab);
    //t = clamp(t, 0., 1.);
    
    vec3 c = a + t*ab;
    
    float x = length(p-c)-r;
    float y = (abs(t-.5)-.5)*length(ab);
    float e = length(max(vec2(x, y), 0.));
    float i = min(max(x, y), 0.);
    
    return e+i;
}

float sdTorus(vec3 p, vec2 r) {
	float x = length(p.xz)-r.x;
    return length(vec2(x, p.y))-r.y;
}

float dBox(vec3 p, vec3 s) {
    p = abs(p)-s;
	return length(max(p, 0.))+min(max(p.x, max(p.y, p.z)), 0.);
}
float sdRoundCone( in vec3 p, in float r1, float r2, float h )
{
    vec2 q = vec2( length(p.xz), p.y );
    
    float b = (r1-r2)/h;
    float a = sqrt(1.0-b*b);
    float k = dot(q,vec2(-b,a));
    
    if( k < 0.0 ) return length(q) - r1;
    if( k > a*h ) return length(q-vec2(0.0,h)) - r2;
        
    return dot(q, vec2(a,b) ) - r1;
}

float sdEllipsoid( in vec3 pos, in vec3 cen, in vec3 rad )
{
    vec3 p = pos - cen;
    float k0 = length(p/rad);
    float k1 = length(p/(rad*rad));
    return k0*(k0-1.0)/k1;
}
float opSmoothUnion( float d1, float d2, float k ) {
    float h = clamp( 0.5 + 0.5*(d2-d1)/k, 0.0, 1.0 );
    return mix( d2, d1, h ) - k*h*(1.0-h); }

float opSmoothSubtraction( float d1, float d2, float k )
{
    return -opSmoothUnion(d1,-d2,k);
}
float smax( float a, float b, float k )
{
	float h = clamp( 0.5 + 0.5*(b-a)/k, 0.0, 1.0 );
	return mix( a, b, h ) + k*h*(1.0-h);
}
float groundPlane(vec3 p) {
  return p.y;
}

float mushroomStem(vec3 p) {
  return sdRoundCone(p - vec3(0.0, 0.3, 0.0), 0.8, 0.3, 2.0);
}

float mushroomHead(vec3 p) {
  float s = sdSphere(p - vec3(0.0, 2.5, 0.0), 0.5);
  float s1 = sdEllipsoid(p - vec3(0.0, 2.5, 0.0), vec3(0.0, 0.0, 0.0), vec3(1.5, 1.2, 1.5));
  float s2 = sdEllipsoid(p - vec3(0.0, 2.0, 0.0), vec3(0.0, 0.0, 0.0), vec3(1.4, 0.8, 1.34));
  s = opSmoothSubtraction(s2, s1, 0.1);
  return opSmoothUnion(s, s, 0.1);
}
float mushroomSpikes(vec3 p) {
  float b1s = sdSphere(p - vec3(0.0, 3.2, -1.0), 0.2);
  float b2s = sdSphere(p - vec3(1.2, 3.0, -0.2), 0.2);
  float b3s = sdSphere(p - vec3(0.3, 3.6, -0.1), 0.2);
  float b4s = sdSphere(p - vec3(0.4, 2.8, 1.3), 0.2);
  float b5s = sdSphere(p - vec3(-1.0, 3.2, 0.5), 0.2);
  float b6s = sdSphere(p - vec3(-1.0, 2.8, -0.8), 0.2);
  float d = opSmoothUnion(b1s, b2s, 0.1);
  d = opSmoothUnion(b3s, d, 0.1);
  d = opSmoothUnion(b4s, d, 0.1);
  d = opSmoothUnion(b5s, d, 0.1);
  return opSmoothUnion(b6s, d, 0.1);
}
float repeatedSphere( vec3 p, vec3 c, float s )
{
  return length( mod(p+0.5*c,c)-0.5*c ) -s;
  //return length(mod(p,c)-.5*c) - s;
}



float sdMushroom(vec3 p){

    //MUSHROOM STEM
    float cr = mushroomStem(p);
    
    //MUSHROOM HEAD
    float s = mushroomHead(p);
    float mushroom = opSmoothUnion(cr,s,0.1);
    mushroom = opSmoothUnion(mushroom,mushroomSpikes(p),0.1);
    
    return mushroom;
}
float sdMushroomRepeat(in vec3 p)
{
    const vec3 repeatInterval = vec3(1.0, 1.0, 1.0); // Define o intervalo de repetição desejado
    
    vec3 pRepeat = mod(p, repeatInterval) - 0.5 * repeatInterval;
    return sdMushroom(pRepeat);
}
float GetDist(vec3 p) {
    
    float t = iTime;
    
    // ground plane
    float pd = groundPlane(p);
    //float md = sdMushroom(p);
    float md = sdMushroomRepeat(p);
    float d = clamp(min(md,pd),0.,1.);
    return md;
}

float RayMarch(vec3 ro, vec3 rd) {
	float dO=0.;
    
    for(int i=0; i<MAX_STEPS; i++) {
    	vec3 p = ro + rd*dO;
        float dS = abs( GetDist(p) );
        dO += dS;
        if(abs(dO)>MAX_DIST || dS<SURF_DIST) break;
    }
    
    return dO;
}

vec3 GetNormal(vec3 p) {
	float d = GetDist(p);
    vec2 e = vec2(.001, 0);
    
    vec3 n = d - vec3(
        GetDist(p-e.xyy),
        GetDist(p-e.yxy),
        GetDist(p-e.yyx));
    
    return normalize(n);
}

float GetLight(vec3 p) {
    vec3 lightPos = vec3(3, 5, 4);
    vec3 l = normalize(lightPos-p);
    vec3 n = GetNormal(p);
    
    float dif = clamp(dot(n, l)*.5+.5, 0., 1.);
    float d = RayMarch(p+n*SURF_DIST*2., l);
    if(p.y<.01 && d<length(lightPos-p)) dif *= .5;
    
    return dif;
}

vec3 R(vec2 uv, vec3 p, vec3 l, float z) {
    vec3 f = normalize(l-p),
        r = normalize(cross(vec3(0,1,0), f)),
        u = cross(f,r),
        c = p+f*z,
        i = c + uv.x*r + uv.y*u,
        d = normalize(i-p);
    return d;
}



void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
    vec2 uv = (fragCoord-.5*iResolution.xy)/iResolution.y;
	vec2 m = iMouse.xy/iResolution.xy;
    
    vec3 col = vec3(0);
    
    vec3 ro = vec3(9.*((sin(iTime)/4.)), 1.5, -3.*(cos(iTime)));
    //vec3 ro = vec3(9.*(sin(iTime)/4.), 4., 8.*(cos(iTime)/4.));
    //ro.yz *= Rot(-m.y+.4);
    //ro.xz *= Rot(iTime*.2-m.x*6.2831);
    
    vec3 rd = R(uv, ro, vec3(0,0,0), .7);

    float d = RayMarch(ro, rd);
    
    if(d<MAX_DIST) {
    	vec3 p = ro + rd * d;
    
    	float dif = GetLight(p);
    	col = vec3(dif);
    }
    
    col = pow(col, vec3(.4545));	// gamma correction
    
    fragColor = vec4(col,1.0);
}

```

# CODIGO TRIANGULOS E ARGOLA
```GLSL
#if 1
mat2 Rot(float a) {
    float s = sin(a);
    float c = cos(a);
    return mat2(c, -s, s, c);
}
float sdBoxFrame( vec3 p, vec3 b, float e)
{
       p = abs(p  )-b;
  vec3 q = abs(p+e)-e;

  return min(min(
      length(max(vec3(p.x,q.y,q.z),0.0))+min(max(p.x,max(q.y,q.z)),0.0),
      length(max(vec3(q.x,p.y,q.z),0.0))+min(max(q.x,max(p.y,q.z)),0.0)),
      length(max(vec3(q.x,q.y,p.z),0.0))+min(max(q.x,max(q.y,p.z)),0.0));
}

float sdSphere(vec3 p, float s){

    return length(p)-s;
}
float sdRoundBox(vec3 p, vec3 b, float r){

    vec3 q = abs(p) - b;
    return length(max(q,0.0)) + min(max(q.x,max(q.y,q.z)),0.0) - r;
}
float sdTorus(vec3 p, vec2 t){

    vec2 q = vec2(length(p.xz)-t.x,p.y);
    return length(q)-t.y;
}
// signed distance to a pyramid of base 1x1 and height h
float sdPyramid( vec3 p, float h)
{
    float m2 = h*h + 0.25;
    
    // symmetry
    p.xz = abs(p.xz); // do p=abs(p) instead for double pyramid
    p.xz = (p.z>p.x) ? p.zx : p.xz;
    p.xz -= 0.5;
	
    // project into face plane (2D)
    vec3 q = vec3( p.z, h*p.y-0.5*p.x, h*p.x+0.5*p.y);
        
    float s = max(-q.x,0.0);
    float t = clamp( (q.y-0.5*q.x)/(m2+0.25), 0.0, 1.0 );
    
    float a = m2*(q.x+s)*(q.x+s) + q.y*q.y;
	float b = m2*(q.x+0.5*t)*(q.x+0.5*t) + (q.y-m2*t)*(q.y-m2*t);
    
    float d2 = max(-q.y,q.x*m2+q.y*0.5) < 0.0 ? 0.0 : min(a,b);
    
    // recover 3D and scale, and add sign
    return sqrt( (d2+q.z*q.z)/m2) * sign(max(q.z,-p.y));;
}
float repeatedPyramid(vec3 p, float h, vec3 c){

    vec3 q = mod(p+0.5*c,c)-0.5*c;
    float m2 = h*h + 0.25;
    // symmetry
    q.xz = abs(q.xz); // do p=abs(p) instead for double pyramid
    q.xz = (q.z>q.x) ? q.zx : q.xz;
    q.xz -= 0.5;
    // project into face plane (2D)
    vec3 qq = vec3( q.z, h*q.y-0.5*q.x, h*q.x+0.5*q.y);
        
    float s = max(-qq.x,0.0);
    float t = clamp( (qq.y-0.5*qq.x)/(m2+0.25), 0.0, 1.0 );
    
    float a = m2*(qq.x+s)*(qq.x+s) + qq.y*qq.y;
	float b = m2*(qq.x+0.5*t)*(qq.x+0.5*t) + (qq.y-m2*t)*(qq.y-m2*t);
    
    float d2 = max(-qq.y,qq.x*m2+qq.y*0.5) < 0.0 ? 0.0 : min(a,b);
    
    // recover 3D and scale, and add sign
    return sqrt( (d2+qq.z*qq.z)/m2 ) * sign(max(qq.z,-q.y));;
}
float repeatedBoxFrame(vec3 p, vec3 b, float e, vec3 c){

        vec3 q = mod(p+0.5*c,c)-0.5*c;
        q = abs(q) - b;
        vec3 qq = abs(q+e) -e;
        return min(min(
      length(max(vec3(q.x,qq.y,qq.z),0.0))+min(max(q.x,max(qq.y,qq.z)),0.0),
      length(max(vec3(qq.x,q.y,qq.z),0.0))+min(max(qq.x,max(q.y,qq.z)),0.0)),
      length(max(vec3(qq.x,qq.y,q.z),0.0))+min(max(qq.x,max(qq.y,q.z)),0.0));
        
}
float repeatedTorus(vec3 p, vec2 t, vec3 c){
    
    //p.xy *= Rot(iTime);
    //p /= 0.5;
    //Adiciona rotação aqui
    vec3 q = mod(p+0.5*c,c)-0.5*c;
    //q.xy *= Rot(iTime);
    vec2 qq = vec2(length(q.xz)-t.x,q.y);
    return length(qq)-t.y;
}
float repeatedRoundBox(vec3 p,vec3 b,vec3 c,float r){
    vec3 q = mod(p+0.5*c,c)-0.5*c;
    vec3 qq = abs(q) - b;
    return length(max(qq,0.0)) + min(max(qq.x,max(qq.y,qq.z)),0.0) - r;
}
float repeatedSphere(vec3 p, vec3 c,float s){
    
    // vec3 q = mod(p+0.5*c,c)-0.5*c;
    // return primitive ( q);
    //REPETINDO O PADRÃO DAS ESFERAS EM TODOS EIXOS
    vec3 t = vec3(mod(p+0.5*c,c)-0.5*c);
    return length(t)-s;
}
#else
float dot2( in vec3 v ) { return dot(v,v); }
float sdBoxFrame( vec3 p, vec3 b, float e)
{
       p = abs(p  )-b;
  vec3 q = abs(p+e)-e;

  return sqrt(min(min(dot2(max(vec3(p.x,q.y,q.z),0.0)),
                      dot2(max(vec3(q.x,p.y,q.z),0.0))),
                      dot2(max(vec3(q.x,q.y,p.z),0.0)))) 
         +min(0.0,min(min( max(p.x,max(q.y,q.z)),
                           max(p.y,max(q.z,q.x))),
                           max(p.z,max(q.x,q.y))));
}
#endif


float map( in vec3 pos )
{
    //return sdBoxFrame(pos, vec3(0.3,0.2,0.3), 0.02);
    //return sdSphere(pos,0.5);
    //Rotação para torus
    vec3 tx = pos - vec3(0.,.2,0.);
    //tx.zy *= Rot(iTime);
    vec3 txx = pos - vec3(0.,.2,0.);
    //txx.xy *= Rot(iTime);
    float tu = repeatedTorus(tx, vec2(0.5,0.025),vec3(1.5));
    //float tv = repeatedTorus(txx, vec2(0.5,0.025),vec3(3.5));
    //float tu = sdTorus(tx,vec2(0.5,0.04));
    //float tv = sdTorus(txx, vec2(0.6,0.04));
    float tt = tu;//min(tu,tv);
    //float x = repeatedSphere(pos+0.3,vec3(1.0,1.0,1.0),0.25);
    //return sdRoundBox(pos,vec3(0.5,0.3,0.5),0.125);
    //float d = repeatedRoundBox(pos,vec3(0.05,0.05,0.05),vec3(1.),0.025);
    //return min(x,d);
    //float tu = repeatedTorus(pos-vec3(1.,1.15,1.), vec2(0.5,0.025),vec3(1.));
    //return min(d,f);
    //return repeatedBoxFrame(pos,vec3(0.3,0.2,0.3),0.02,vec3(2.,1.0,3.5));
    //pos *=1.6;
    
    //scale pyramid
    //float x = sdPyramid(pos/0.5,.9)*0.5;
    
    float py = repeatedPyramid(pos/0.5,.9,vec3(3.5))*0.5;
    return min(tt,py);
}

// https://iquilezles.org/articles/normalsSDF
vec3 calcNormal( in vec3 pos )
{
    vec2 e = vec2(1.0,-1.0)*0.5773;
    const float eps = 0.0005;
    return normalize( e.xyy*map( pos + e.xyy*eps ) + 
					  e.yyx*map( pos + e.yyx*eps ) + 
					  e.yxy*map( pos + e.yxy*eps ) + 
					  e.xxx*map( pos + e.xxx*eps ) );
}
    
#if HW_PERFORMANCE==0
#define AA 1
#else
#define AA 3
#endif

void mainImage( out vec4 fragColor, in vec2 fragCoord )
{
     // camera movement	
	float an = 0.5*(iTime-10.0);
	vec3 ro = 2.*vec3( 1.0*cos(an), .2, 1.0*sin(an) );
    vec3 ta = vec3( 0.0, 0.0, 0.0 );
    // camera matrix
    vec3 ww = normalize( ta - ro );
    vec3 uu = normalize( cross(ww,vec3(0.0,1.0,0.0) ) );
    vec3 vv = normalize( cross(uu,ww));
   
    // render    
    vec3 tot = vec3(0.0);
    #if AA>1
    for( int m=0; m<AA; m++ )
    for( int n=0; n<AA; n++ )
    {
        // pixel coordinates
        vec2 o = vec2(float(m),float(n)) / float(AA) - 0.5;
        vec2 p = (2.0*(fragCoord+o)-iResolution.xy)/iResolution.y;
        #else    
        vec2 p = (2.0*fragCoord-iResolution.xy)/iResolution.y;
        #endif

	    // create view ray
        vec3 rd = normalize( p.x*uu + p.y*vv + 1.5*ww );

        // raymarch
        const float tmax = 10.0;
        float t = 0.0;
        for( int i=0; i<100; i++ )
        {
            vec3 pos = ro + t*rd;
            float h = map(pos);
            if( h<0.0001 || t>tmax ) break;
            t += h;
        }
        
    
        // shading/lighting	
        vec3 col = vec3(0.0);
        if( t<tmax )
        {
            vec3 pos = ro + t*rd;
            vec3 nor = calcNormal(pos);
            float dif = clamp( dot(nor,vec3(0.57703)), 0.0, 1.0 );
            float amb = 0.5 + 0.5*dot(nor,vec3(0.0,1.0,0.0));
            col = vec3(0.2,0.3,0.4)*amb + vec3(0.85,0.75,0.65)*dif;
        }

        // gamma        
        col = sqrt( col );
	    tot += col;
    #if AA>1
    }
    tot /= float(AA*AA);
    #endif

	fragColor = vec4( tot, 1.0 );
}
```

