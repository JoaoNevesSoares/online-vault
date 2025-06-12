In this work, a cost-aware job scheduling approach based on queueing theory in hybrid clouds is proposed.

job scheduling problem in private cloud is modeled as  a queueing model.
genetic algorithm is applied to achieve optimal queues for jobs to improve usage rate in private cloud.
Our cost-aware job scheduling algorithm can reduce the average job waiting time and average job response time in the private cloud.

A cost-aware job scheduling approach based on queueing theory in hybrid clouds is proposed.
the main ideia:
jobs  are  dispatched  to  corresponding  job  queues  in  the private cloud. If the private cloud cannot meet the demands of  users,  the  public  cloud  with  the  cheapest  costs  will  be rented. Therefore, the utilization rate of the private cloud is improved and total costs of hybrid clouds drop greatly.

The Hadoop 2.7.1 is adopted to perform the experiment.



ChunLin Li e seu grupo fizeram algumas contribuições relevantes a respeito de otimizações de escalonamento de tarefas por cloud bursting. Em \cite{Chunlin2015-bh} propõem um novo modelo hierárquico de escalonador em nuvem híbrida que leva em consideração tanto os grupos de aplicativos em nuvem privada quanto os provedores de nuvem pública. Em \cite{Chunlin2018} they aimed at the private cloud scheduling problem, proposing a cost-aware job scheduling approach based on queueing theory. It includes a load balancing job scheduling algorithm based on a genetic algorithm (GA) to dispatch jobs to optimal queues in private clouds in order to improve the utilization rate of private resources.





Eles introduziram um modelo matemático para avaliar o desempenho das aplicações em cada grupo.\ups{Olha só: isso é importante destacar, neste trabalho a validação se deu por modelos matemáticos.} Além disso, eles compararam com um escalonador QoS da literatura e constataram um melhor desempenho. \cite{Chunlin2019-mc} eles abordam ... Outro trabalho na mesma linha foi apresentado por \cite{Lee2017-vo}


propõem o algoritmo MOSACO (Multi-Objective Scheduling Algorithm based on Ant Colony Optimization) para otimização da tarefa de escalonamento de recursos em ambientes de nuvem híbrida. A solução proposta considera as restrições de prazo e de custos financeiros como métricas para 

No trabalho "Multi-Objective Scheduling algorithm based on Ant Colony Optimization (MOSACO)" os autores adotam duas estratégias de otimização: "cost-first" e "time-first" que considera tanto as restrições de tempo das aplicações quanto as restrições de custos para realizar escalonamento de tarefas em nuvem híbrida. Eles também apresentam um modelo de otimização de entropia baseada em colônia de formigas visando atender os requisitos de QoS das aplicações com ênfase em maximizar os interesses dos usuários e dos provedores de recursos.  

The task-oriented Multi-Objective Scheduling algorithm based on Ant Colony Optimization (MOSACO) is proposed to minimize task completion time and costs using time-first and cost-first single-objective optimization strategies, respectively. The algorithm uses an entropy optimization model to maximize user service quality and resource provider profitability.


[12] proposed a new task-oriented multiobjective scheduling method based on ant colony optimization for scheduling the resources. They provide the most elevated optimality and for minimizing the completion time and cost when compared with the similar scheduling methods.

Zuo et al. [302] proposed multi-objective hybrid cloud resource scheduling based on ant colony optimization (MOSAC) with deadline and cost constraints.