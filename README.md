# Q-leaning_sarsa
## 1
¿Cómo afecta una  α baja (0.01) vs. una alta (0.9) a la velocidad con la que las curvas de recompensa (gráfica plot_rewards) se estabilizan?
\(\alpha\) baja (0.01):
El aprendizaje es muy lento.
La curva de recompensas sube y se estabiliza despacio.
El agente necesita muchos más episodios para aprender una buena política.
La media móvil de la recompensa mejora poco a poco.
\(\alpha\) alta (0.9):
El aprendizaje es muy rápido al principio.

 ¿Observas inestabilidad (fluctuaciones grandes y erráticas en la recompensa incluso al final del entrenamiento) con valores altos de 
α? ¿Por qué podría ocurrir esto?

Sí, con \(\alpha\) alta (0.9) es común ver inestabilidad:
La curva de recompensas puede mostrar grandes picos y caídas incluso después de muchos episodios.
Esto ocurre porque el agente sobreescribe lo aprendido con cada nueva experiencia, dando mucho peso a la recompensa más reciente y poco a la experiencia acumulada.
Si el entorno es estocástico o el agente explora, los valores Q pueden fluctuar mucho.

Compara las Policy Grids finales para α=0.01 y α= 0.5 ¿Cuál parece haber aprendido una ruta más definida hacia la meta G, dado el número de episodios actual? ¿Sugiere esto que una 
α baja podría necesitar más episodios?
\(\alpha=0.01\):
La Policy Grid suele mostrar una política difusa o poco definida.
El agente puede no haber aprendido aún el camino óptimo a la meta G.
Sí, una \(\alpha\) baja necesita más episodios para converger a una política clara.
\(\alpha=0.5\):
La Policy Grid muestra una ruta más definida y consistente hacia la meta.
El agente aprende más rápido y la política se estabiliza antes.
