### Fundamentos de la base de datos

- la base de datos está compuesta por tres sistemas:
    - recursos
    - delegaciones
    - iniciativas
- existen otros sistemas ya diseñados, pero no están implementados aún:
    - personas
    - privilegios
    - historial
    - conocimiento
- usamos YAML como formato para todos los elementos porque está pensado para ser fácilmente legible y editable por humanos y también por máquinas en simultáneo
- usamos git porque nos da hosting, acceso colaborativo, control de versiones y una API gratis, entre otras cosas
- ID de la base de datos = nombre de archivo = nombre del elemento. un identificador, tres propósitos. reduce la complejidad
- para facilidad de uso, la mayoría de los campos pueden estar vacíos y son de formato libre (el contenido puede tener cualquier forma)
- las referencias, que son un sistema intencionalmente minimalista para facilidad de uso, facilitarán la coordinación de la organización si sus actividades se escalan
- la separación de sistemas es para mantener contribución, autoridad y confianza separados, pero también permite la delegación prolija, modularidad y modificación sobre la marcha
- el resto de elecciones de diseño están a continuación, aunque no muy explicadas

### Uso de la base de datos

- propiedades de los elementos
    - 1 elemento = 1 archivo con extensión ".yaml"
    - ID de la base de datos = nombre de archivo = nombre del elemento. un identificador, tres propósitos
        - en cualquier parte de esta guía esas tres palabras son intercambiables
        - requisitos
            - deben ser nombres legibles y entendibles
            - se escriben en minúscula y sin espacios
            - usan guiones para separar palabras
        - ejemplo: "servidor-principal.yaml"
    - no puede haber dos elementos con el mismo ID en toda la base de datos entera

- propiedades del contenido de los elementos
    - el formato de YAML de los objetos debe ser respetado
        - los campos que son listas deben seguir siendo listas
        - los campos que son un sólo string de texto deben seguir siendo tal
        - la sintaxis YAML debe ser correcta
    - cada sistema tiene su propia taxonomía
        - la taxonomía define qué significa cada campo (por ej. "detalle") y qué corresponde poner en él
        - no se deberían agregar o restar campos en ningún caso
    - la mayoría de los campos son de formato libre
        - esto significa que no están limitados a una lista de valores / formato predeterminado y el contenido puede tener cualquier forma (mientras respete el tipo de objeto YAML requerido)
        - por supuesto, cada campo sigue teniendo un significado y un propósito definido por la taxonomía que debe respetarse
        - si un campo no es de formato libre, estará indicado como "FORMATO ESTRICTO" en la guía de la taxonomía junto con cómo debe llenarse
            - cuando una taxonomía permite "otro", se puede especificar el valor correspondiente de ser adecuado / necesario
                - esa opción es específicamente para cuando un campo de formato estricto no permite lo que se debe introducir
                    - por ejemplo, en casos excepcionales no contemplados por las opciones de ese campo de formato estricto
    - la mayoría de los campos pueden estar vacíos
        - cuando corresponda, se puede utilizar un string vacío: ""
        - no es necesario inventar información para llenar un campo que todavía no se conoce
        - dejar un campo vacío es preferible a introducir información falsa. la información especulativa es aceptable, pero debe entenderse que es tal
    - referencias
        - se hacen mediante IDs
        - una referencia se escribe entre dobles corchetes: [[id]]
            - ej. [[iniciativa-ejemplo]], [[recurso-ejemplo]], [[delegacion-ejemplo]]
        - las referencias deben utilizarse siempre que sea relevante y posible
            - nos ahorrará trabajo en el futuro que ya haya referencias hechas desde el día 1
        - se puede hacer referencias entre sistemas, y muchas veces va a ser necesario
        - las referencias deben apuntar a elementos existentes
        - cuando se cambia un ID, deben actualizarse las referencias que apuntan al ID anterior
            - esto será automatizado eventualmente. por ahora, sólo hay que buscar "[[id]]" en la base de datos para encontrar referencias y cambiarlas manualmente
        - conviene evitar duplicar información innecesariamente entre sistemas
            - cuando un elemento de un sistema está relacionado con otro, utilizar una referencia en lugar de copiar su información

- el anidado de directorios de la base de datos no tiene reglas
    - hay sistemas que expresamente permiten el anidado de sus elementos y están pensados con anidado en mente, y hay otros que no
    - el anidado de los elementos en la base de datos no está ligado a u obligado a seguir el de los directorios, y puede hacerse como se desee
    - aún así puede ser confuso si no están organizados de forma similar, por ejemplo en los sistemas que soportan ambos tipos de anidados. recomendamos que haya estructura

- los sistemas no necesitan formalizar todas sus interacciones
    - cada sistema registra los hechos que le corresponden y las relaciones relevantes deberían poder expresarse mediante referencias entre elementos
    - las interacciones entre sistemas son más que nada informales, y luego se ven reflejadas en los datos

- tener en cuenta: se supone que estos sistemas se conformen a la realidad y no viceversa
    - la realidad es mucho más compleja e informal que este sistema y no es inteligente intentar evitarlo
    - el objetivo de esta base de datos entera es poder mantener una visión estratégica de la organización al escalar sus actividades

- en la práctica
    - las guías de cada sistema sirven como referencia para crear nuevos elementos
    - las plantillas de cada sistema sirven para copiar y pegar en un elemento nuevo al crearlo para llenar su información

- no poner contraseñas, tokens, claves privadas u otros secretos en la base de datos, ya que es pública

- la base de datos debe ser mantenida con tal de que siga reflejando la realidad
