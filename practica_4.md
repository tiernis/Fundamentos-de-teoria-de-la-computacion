# Reducciones de problemas. MT restringidas

1. Considerando la reducción de HP a Lᵤ descripta en clase, responder:
    1. Explicar por qué la función identidad, es decir la función que a toda cadena le asigna la misma cadena, no es una reducción de HP a Lᵤ.

        Porque, si bien no hay problema para el caso en que acepta, loopea o es una cadena inválida, cuando M para sobre w en qᵣ en HP, el par (<M>,w) ∈ a HP pero ∉ a Lᵤ.

    2. Explicar por qué las MT M\` generadas en los pares (<M\`>, w) de Lᵤ, o bien paran aceptando, o bien loopean.

        Porque la propia implementación hace que las máquinas paren aceptando o loopeen ya que cambian el estado qᵣ por qₐ de modo que la máquina siempre acepta en Lᵤ(si aceptaba o rechazaba en HP) o loopea(si ya loopeaba en HP).

    3. Explicar por qué la función utilizada para reducir HP a Lᵤ también sirve para reducir HPᶜ a Lᵤᶜ.

        A priori, hay una propiedad que dice que L₁ α L₂ ↔ L₁ᶜ α L₂ᶜ por lo que puedo usar la misma función de reducción en ambos casos. Más específicamente, en este caso, necesito una función para todo lo que no sea HP y todo lo que no sea Lᵤ. Se dan los mismos casos que arriba: si la máquina dentro de HPᶜ rechaza o acepta, la función lo cambiará por algo que Lᵤᶜ acepte siempre. Si llega un w inválido, será inválido para ámbos.

    4. Explicar por qué la función utilizada para reducir HP a Lᵤ no sirve para reducir Lᵤ a HP.

        Igual que en el caso anterior, a priori hay una propiedad que dice que sea L ∈ R, se da que L α Lᵤ, pero esto no implica que Lᵤ α L, ya que eso supondría que L es "tan o más dificil" que Lᵤ, y lo cierto es que Lᵤ ∉ R, por lo que claramente Lᵤ es más dificil que L. Por otro lado, remitiéndonos a la función en sí misma, si tengo que reducir de Lᵤ a HP usando la misma función que usé para reducir de HP a Lᵤ, entonces se da que:
        * Para el caso en que Lᵤ acepte, no habrá problema.
        * Si la cadena no es válida tampoco habrá problema.
        * El problema aparecerá cuando M pare sobre w en qᵣ en Lᵤ y la función convierta ese input en algo que esté dentro de HP y no se cumpla la propiedad de reducción.

    5. Explicar por qué si el input v de la MT M<sub>f</sub> que computa la función de reducción no tiene la forma (\<M>, w), no es correcto que M<sub>f</sub> genere, en lugar de la cadena 1, un par de la forma (<M<sub>Ʃ*</sub>>, v), siendo M<sub>Ʃ*</sub> una MT que acepta todas las cadenas.

        El problema es que M<sub>Ʃ*</sub> es una máquina de Turing que acepta todo, por lo que, le llegue en input que le llegue va parar en qₐ y no se va a cumplir la propiedad de la reducción.

    6. Explicar por qué la siguiente MT M<sub>f</sub> no computa una reducción de HP a Lᵤ dado v:
        * Si v no tiene la forma (\<M>, w), entonces M<sub>f</sub> genera el output 1.
        * Si v tiene la forma (\<M>,w), entonces M<sub>f</sub> ejecuta M sobre w, y, si M acepta w, entonces genera el output (\<M>,w); y, si M rechaza w, entonces genera el output 1.

        A priori, esta función no es computable porque no tiene en cuenta qué hacer en caso de loops. Suponiendo que fuera computable(que eso se hubiera resuelto de algún modo), la función no reduciría a Lᵤ porque, si v tiene la forma (\<M>,w), M<sub>f</sub> ejecuta M sobre w y M rechaza w, entonces M<sub>f</sub> debe, para el caso en que M rechace w, generar un output que Lᵤ acepte(y 1 no es un output que Lᵤ acepte).

2. Probar el caso (b) del teorema presentado en clase, que enuncia:
    * Caso (a): Si L₁ α L₂ entonces L₂ ∈ R ⟶ L₁ ∈ R.
    * Caso (b): Si L₁ α L₂ entonces L₂ ∈ RE ⟶ L₁ ∈ RE.

    *Ayuda: basarse en la demostración del caso (a) desarrollada en clase.*

    La idea general es que si existe una MT M<sub>f</sub> que reduce L₁ a L₂, y existe una MT M₂ que acepta L₂, entonces también existe una MT M₁ que acepta L₁: la que ejecuta primero M<sub>f</sub> sobre el input w y luego M₂ sobre el output f(w) de M<sub>f</sub>. Para este caso, en particular, la MT M₂ puede parar o no, y por lo tanto, también la MT M₁.  
    La prueba formal es la siguiente:
    * Supongamos que L₁ α L₂ y L₂ ∈ RE. Veamos si se cumple L₁ ∈ RE.
    * Por la hipótesis:
        * Existe una MT M<sub>f</sub> que computa una función que cumple w ∈ L₁ ↔ f(w) ∈ L₂.
        * Existe una MT M₂ que acepta L₂ y puede parar o no.
    * Así también, existe una MT M₁ que acepta L₁ y puede parar o no, por lo que:
        * Dado un input w.
        * M₁ ejecuta primero M<sub>f</sub> sobre w para obtener f(w).
        * Luego ejecuta M₂ sobre f(w).
        * Y acepta si y solo si M₂ acepta.
    * M₁ podría no parar porque M<sub>f</sub> y M₂ tampoco podrían necesariamente parar.
    * L₁=L(M₁) ya que w ∈ L₁ ↔ M<sub>f</sub>, a partir de w, computa f(w) ∈ L₂ ↔ M₂ acepta f(w) ↔ M₁ acepta w ↔ w ∈ L(M₁).

3. Considerando la reducción de Lᵤ a L<sub>Ʃ*</sub> descripta en clase, responder:
    1. Explicar por qué no sirve como función de reducción la función siguiente: a todo input le asigna como output el código <M<sub>Ʃ*</sub>>.

        El problema está en algo que está afuera de Lᵤ, un w inválido. La función lo transformaría en algo válido y no se cumpliría la función de Lᵤ.

    2. Explicar por qué la reducción descripta en clase no sirve para probar que L<sub>Ʃ*</sub> ∉ RE.

        Porque Lᵤ ∈ RE. Para probar que L<sub>Ʃ*</sub> ∉ RE hay que reducirlo usando un lenguaje que ∉ RE.

4. Probar formalmente que las funciones de reducción gozan de la propiedad transitiva.
*Ayuda: revisar la idea general comentada en clase; también basarse en la prueba que se haya desarrollado para el 2, porque debería ser similar.*

    Hay que probar que si L₁ α L₂ y L₂ α L₃, entonces L₁ α L₃. Para probar tal afirmación voy a construir una MT f1, que representa la función de reducción de L₁, que reciba un par (<M>, w). El input que recibe f1 será procesado por una MT f2, que representa la función de reducción de L₂, que podrá aceptar o rechazar. Si f2 rechaza, f1 también lo hará. Si f2 acepta, el output será procesado por una MT f3, que representará la función de reducción de L₃. Al igual que f2, si f3 rechaza, también lo hará f1. Si f3 acepta, también lo hará f1 y se probará la transitividad.

5. Sea el lenguaje Dₕₚ = {wᵢ | Mipara desde wᵢ, según el orden canónico}. Encontrar una reducción de Dₕₚ a HP.

6. Sea el lenguaje L<sub>∅</sub> = {<M>| L(M) = ∅}. Responder:
    1. Encontrar una reducción de Lᵤᶜ a L<sub>∅</sub>.  
    _Ayuda: basarse en la idea de la reducción de Lᵤ a L<sub>Ʃ*</sub>, es muy similar._
    2. Considerando la reducción desarrollada en (1) ¿Qué se puede decir de L<sub>∅</sub>, a qué clase de la jerarquía de la computabilidad pertenece?

7. Construir un autómata finito que reconozca el lenguaje de las cadenas de {0, 1}*, es decir todas las cadenas de 0 y 1 de cualquier tamaño incluso la vacía, tales que a todo cero le siga un uno.  
*Ayuda: En general conviene primero construir el diagrama de transición de estados, porque da una idea de cómo construir el autómata finito.*

8. Un autómata linealmente acotado(ALA) es una MT con una sola cinta con la restricción de que su cabezal sólo puede leer y escribir en las celdas en que se encuentra el input. Probar que el lenguaje aceptado por un ALA es recursivo.

*Ayuda: ¿En cuántos pasos se puede detectar que el ALA entra en loop?*

    Es recursivo porque puede construirse una MT que siempre para. El truco está en usar una cota de pasos, entonces, el lenguaje acepta si no supera la cota; caso contrario, rechaza.