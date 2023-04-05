<h1>2CNN balls classification</h1>
<h2>Introducción</h2>
<p>En este trabajo el objetivo ha sido crear una RED NEURONAL CONVOLUTIVA capaz de clasificar un conjunto de datos determinados. </p>
<hr>
<p>Se ha escogido un conjunto de datos proveniente de Kaggle1, que originalmente consistía en una serie de 26 tipos de bolas diferentes.

Se han escogido 5 clases de estas: bolas de béisbol, pelotas de baloncesto, pelotas de playa, bolas de billar y bolas de bolos. Además hay otro conjunto distinto para verificación.

  Cada clase tiene en torno a 110 elementos, a los que además se les aplica Data Augmentation, consistente en cambiar las características de cada imagen (rotándolas, cambiando su brillo…) para obtener lo que esencialmente son nuevos elementos sin mayor esfuerzo, siendo además una buena técnica para evitar el sobreajuste de la red, pues debe tomar en cuenta más orientaciones y es más complicado que “se aprenda las posibilidades de memoria”. Como función de activación de las neuronas utilizaremos la función relu, que es sencillamente 𝑟𝑒𝑙𝑢(𝑥) = 𝑥 · 𝑠𝑖𝑔𝑛(𝑥)+1 2 .

  Por su parte, la función de salida que emplearemos es la softmax, que es 𝑠𝑜𝑓𝑡𝑚𝑎𝑥(𝑥𝑖 ) = 𝑒 𝑥𝑖 ∑ 𝑒 𝑥𝑗 𝑗 , que potencia la cercanía de la salida al one-hot. Por último, y como es habitual para el softmax, como función de pérdida usaremos la entropía categórica cruzada: 𝑑(𝑦, 𝑦̂) = − ∑𝑖 𝑦𝑖 · 𝑙𝑜𝑔(𝑦̂𝑖 ).

  Antes de analizar resultados probaremos varias configuraciones de hiperparámetros de la red y nos quedaremos con la mejor. Después graficaremos la evolución de la precisión y mostraremos la matriz de confusión para analizar los resultados.</p>
 <h2>Colaboradores</h2>
 <em>Alberto Melián Rodríguez</em>
 <em>Federico Colleluori</em>
