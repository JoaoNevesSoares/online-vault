
> [!info] método que define a carga de trabalho com base na Classe
```C
void write_ep_info(FILE *fp, char class)

{

/* easiest way (given the way the benchmark is written)

* is to specify log of number of grid points in each

* direction m1, m2, m3. nt is the number of iterations

*/

int m;

if (class == 'S') { m = 24; }

else if (class == 'W') { m = 25; }

else if (class == 'A') { m = 28; }

else if (class == 'B') { m = 30; }

else if (class == 'C') { m = 32; }

else {

printf("setparams: Internal error: invalid class type %c\n", class);

exit(1);

}

  

fprintf(fp, "%scharacter class\n",FINDENT);

fprintf(fp, "%sparameter (class =\'%c\')\n",

FINDENT, class);

fprintf(fp, "%sinteger m\n", FINDENT);

fprintf(fp, "%sparameter (m=%d)\n", FINDENT, m);

}
```

>M is the Log_2 of the number of complex pairs of uniform (0, 1) random
numbers.  MK is the Log_2 of the size of each batch of uniform random numbers.  MK can be set for convenience on a given system, since it does not affect the results.
- M = log_2(n)
- MK é o log_2 do tamanho de cada "lote" de números aleatórios

> [!info] Variáveis Fortran
> - Double:
> 	- a,an,dum(3),epsilon,gc,mops,q,s,sx,sy,t1,t2,t3,t4,timer_read,tm,tt,x,x1,x2
> - integer:
> 	- i,ierr,ierrcode,ik,j,k,k_offset,kk,l,mk,mm,nit,nk,nn,no_large_nodes,no_nodes,node,np,np_add,nq
> - boolean:
> 	- timers_enabled, verified
> - parameter: {linha 70 ep.f, linha 98-103 ep.cpp}
> 	- timers_enabled = false
> - external:
> 	- randlc(), timer_read()
> - 

>[!info] Variáveis em ep.cpp que não existem no ep.f
> - Double:
> 	-sx_verify_value, sy_verify_value, sx_err, sy_err
> - Char:
> 	- size[16];
> 

```fortran
common/storage/ x(2*nk), q(0:nq-1), qq(10000)
data dum /1.d0, 1.d0, 1.d0/
```
- [data](https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vn85/index.html)
- [common](https://docs.oracle.com/cd/E19957-01/805-4939/6j4m0vn7v/index.html)
> Equivalente em CPP:
> ```cpp
> //common/storage/ x(2*nk)
> //common/storage/ q(0:nq-1)
> #define NK (1 << MK)
> #define NK_PLUS ((2*NK)+1)
> #define NQ 10 #ifdefined(DO_NOT_ALLOCATE_ARRAYS_WITH_DYNAMIC_MEMORY_AND_AS_SINGLE_DIMENSION)
> static double x[NK_PLUS];
> static double q[NQ];
> #else
> static double (*x)=(double*)malloc(sizeof(double)*(NK_PLUS));
> static double (*q)=(double*)malloc(sizeof(double)*(NQ));
> #endif
> //common/storage qq(10000)
> // aparantemente não encontrado
> 
> ```

