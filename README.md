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

## 2

 ¿La política de SARSA se vuelve más "conservadora" o más "directa" con \(\gamma=0.90\)?
Con \(\gamma=0.99\):
SARSA tiende a ser más conservador: evita el acantilado, prefiere rutas largas y seguras, porque penalizaciones futuras (caer al acantilado) pesan mucho en su cálculo.
Con \(\gamma=0.90\):
La política de SARSA se vuelve más directa: el agente se arriesga más a ir cerca del acantilado, porque las penalizaciones lejanas (caer en el futuro) tienen menos peso.

¿Por qué? Un  γ bajo hace que el agente “olvide” o le importe menos lo que pase después de varios pasos, así que prioriza llegar rápido a la meta aunque eso implique más riesgo.
En resumen:
\(\gamma\) bajo → política más directa y arriesgada.
\(\gamma\) alto → política más conservadora y segura.

¿Esperarías que el cambio en \(\gamma\) afecte más a SARSA o a Q-Learning en este entorno?

SARSA:
Es más sensible al cambio de  γ porque su política es on-policy y refleja el riesgo real de caer al acantilado debido a la exploración.
Con  γ  bajo, SARSA “olvida” el peligro de caer en el futuro y se arriesga más.
Q-Learning:
Es off-policy y aprende la política óptima suponiendo que siempre tomará la mejor acción, así que tiende a ir por el borde del acantilado de todos modos.
El cambio de γ afecta, pero menos: Q-Learning sigue buscando el camino más corto, aunque el valor de ese camino cambie un poco.
Justificación:
SARSA incorpora el riesgo de exploración en su política, así que si el futuro importa menos, el agente se arriesga más.
Q-Learning, al ser off-policy, “asume” que no caerá si sigue la mejor acción, así que su política cambia menos.
