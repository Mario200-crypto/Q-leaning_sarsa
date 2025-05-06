# Q-leaning_sarsa
## 1

### 1
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

### 2
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


### 3

¿Cómo se refleja un decaimiento más rápido (0.99) en la curva de recompensa inicial comparado con uno más lento (0.9999)?

Decaimiento rápido (epsilon_decay = 0.99):

ϵ baja rápidamente, el agente explora mucho solo al principio y luego casi siempre explota (elige la mejor acción conocida).
Curva de recompensa inicial: Sube rápido, pero puede estabilizarse pronto y quedarse “atascada” si la política aprendida no es óptima.
Riesgo: Si el agente deja de explorar demasiado pronto, puede quedarse con una política subóptima (por ejemplo, un camino largo pero seguro en vez del óptimo).
Decaimiento lento (epsilon_decay = 0.9999):

ϵ baja muy lentamente, el agente sigue explorando durante muchos episodios.
Curva de recompensa inicial: Sube más despacio, pero el agente tiene más oportunidades de descubrir mejores caminos.
Ventaja: Es más probable que encuentre la política óptima, aunque tarde más en estabilizarse.

¿Qué agente podría “estancarse” en una solución subóptima si deja de explorar demasiado pronto?

Ambos agentes pueden estancarse, pero es más notorio en Q-Learning:
Q-Learning, al ser off-policy, puede aprender un camino óptimo solo si lo explora lo suficiente. Si deja de explorar pronto, puede quedarse con un camino seguro pero subóptimo.
SARSA, al ser on-policy, también puede estancarse, pero su política suele ser más conservadora y puede tardar más en encontrar el óptimo si explora poco.

¿Hay alguna diferencia visible en el rendimiento final o la política si epsilon_min es 0.0? ¿Cuándo podría ser beneficioso mantener un mínimo de exploración incluso después de muchas episodios?
epsilon_min = 0.0:
El agente deja de explorar completamente después de cierto punto.
Riesgo: Si la Q-table no ha convergido o hay cambios en el entorno, el agente nunca descubrirá mejores caminos.
Política: Puede quedarse fija en una política subóptima.
epsilon_min = 0.01:
El agente siempre tiene una pequeña probabilidad de explorar, incluso después de muchos episodios.
Ventaja: Puede descubrir mejores caminos o adaptarse si el entorno cambia.
Rendimiento: Puede haber pequeñas caídas ocasionales en la recompensa (por la exploración), pero es más robusto a cambios y menos propenso a estancarse.

### 4

¿Consigue el agente SARSA llegar a la meta consistentemente durante el renderizado, o se queda atascado en bucles?
Con solo 300 episodios:
Es muy probable que SARSA no llegue consistentemente a la meta durante la fase de renderizado.
En muchos casos, el agente puede quedarse atrapado en bucles en la zona segura (alejado del acantilado), repitiendo movimientos sin acercarse a la meta, o tomando rutas largas y poco eficientes.
¿Por qué?
SARSA es un algoritmo on-policy y, con pocos episodios, la Q-table no ha convergido lo suficiente para distinguir claramente entre caminos seguros y caminos óptimos.
Además, la penalización por caer al acantilado puede hacer que el agente “tema” acercarse a la meta y prefiera moverse en zonas seguras, incluso si eso significa no llegar nunca.

Compara la Policy Grid con la obtenida con 2000 episodios. ¿Por qué la falta de episodios afecta más a SARSA en este escenario para encontrar una ruta funcional?

Policy Grid con 300 episodios:
Las flechas suelen mostrar rutas que evitan el acantilado, pero no necesariamente llevan a la meta.
Puede haber bucles o movimientos repetitivos en la zona segura.
La política es difusa, poco definida, y a veces ni siquiera apunta hacia la meta.
Policy Grid con 2000 episodios:
La política es mucho más clara y definida.
El agente encuentra rutas funcionales (aunque sean largas y seguras), y en muchos casos logra llegar a la meta de forma consistente.
Las flechas muestran un camino coherente hacia la meta, rodeando el acantilado.
¿Por qué SARSA necesita más episodios?
SARSA incorpora el riesgo de exploración en su política (on-policy).
Con pocos episodios, la penalización por caer al acantilado “asusta” al agente y lo hace evitar la zona peligrosa, pero aún no ha aprendido a distinguir entre moverse seguro y avanzar hacia la meta.
Q-Learning (off-policy) aprende más rápido el camino óptimo porque “asume” que siempre tomará la mejor acción, pero SARSA necesita más experiencia para balancear seguridad y progreso hacia la meta.


