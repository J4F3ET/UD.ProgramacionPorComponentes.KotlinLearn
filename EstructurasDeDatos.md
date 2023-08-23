
| Estructura de Datos | Características Principales | Uso Recomendado |
|---------------------|----------------------------|-----------------|
| Array               | - Tamaño fijo.<br>- Acceso rápido por índice.<br>- Inflexible en términos de tamaño.<br>- Inserción/borrado costoso (en el peor caso). | - Cuando el tamaño es constante y no cambiará.<br>- Cuando se requiere acceso rápido por índice.<br>- Bucles simples con iteraciones. |
| ArrayList           | - Tamaño dinámico.<br>- Acceso rápido por índice.<br>- Inserción/borrado lento en posiciones intermedias. | - Para listas que crecerán o cambiarán de tamaño.<br>- Acceso rápido por índice.<br>- Iteraciones simples y accesos aleatorios. |
| LinkedList          | - Tamaño dinámico.<br>- Inserción/borrado rápido en cualquier posición.<br>- Acceso lento por índice. | - Para inserciones/borrados frecuentes en cualquier posición.<br>- Cuando el acceso por índice no es crucial.<br>- Listas que pueden crecer sin restricciones. |
| HashSet             | - Almacena elementos únicos.<br>- No garantiza un orden específico.<br>- Búsqueda y adición rápida. | - Cuando necesitas mantener una colección de elementos únicos.<br>- Búsqueda y adición eficiente son importantes.<br>- El orden de los elementos no es relevante. |
| LinkedHashSet       | - Almacena elementos únicos.<br>- Mantiene el orden de inserción.<br>- Operaciones de búsqueda y adición son más lentas que en HashSet. | - Cuando necesitas mantener elementos únicos en el orden en que fueron agregados.<br>- Búsqueda y adición eficiente siguen siendo importantes.<br>- El orden de inserción es relevante. |
| TreeSet             | - Almacena elementos únicos.<br>- Mantiene los elementos en orden natural o según un comparador.<br>- Búsqueda, adición y eliminación eficientes, pero más lentas que HashSet. | - Cuando necesitas mantener elementos únicos en un orden específico (natural o personalizado).<br>- Requiere operaciones de búsqueda, adición y eliminación eficientes.<br>- El rendimiento es más crítico que en HashSet. |
| HashMap             | - Almacena pares clave-valor.<br>- Búsqueda y adición rápida por clave.<br>- No garantiza un orden específico. | - Cuando necesitas almacenar datos como pares clave-valor.<br>- Búsqueda y adición eficiente por clave.<br>- El orden de los pares clave-valor no es relevante. |
| LinkedHashMap     | - Almacena pares clave-valor.<br>- Mantiene el orden de inserción o un orden de acceso.<br>- Operaciones ligeramente más lentas que en HashMap. | - Cuando necesitas almacenar pares clave-valor en el orden en que se agregaron.<br>- Mantener el orden de inserción o de acceso es importante.<br>- Las operaciones ligeramente más lentas no son un problema. |
| TreeMap             | - Almacena pares clave-valor.<br>- Mantiene los pares en orden natural o según un comparador.<br>- Operaciones más lentas que en HashMap. | - Cuando necesitas almacenar pares clave-valor en un orden específico (natural o personalizado).<br>- Requiere operaciones de búsqueda, adición y eliminación eficientes en un contexto ordenado.<br>- El rendimiento es más crítico que en HashMap. |