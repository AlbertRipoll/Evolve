README.txt
==========

Este documento resume el análisis exploratorio y la limpieza de un conjunto de datos de gastos personales registrados por un usuario entre septiembre de 2021 y noviembre de 2025.

Fuente de los datos
-------------------
Los datos provienen de dos fuentes aunque solo se analiza la primera:
- La app móvil "Money Manager", donde se registraron transacciones (gastos e ingresos compartidos).
- Una hoja de cálculo en Google Drive, donde se anotaron principalmente gastos relacionados con el uso de vehículos (gasolina, peajes, reparaciones, etc.).

Estructura inicial del dataset
------------------------------
El dataset original contiene 1.402 registros y 5 columnas:
- Date: fecha de la transacción (formato YYYY-MM-DD).
- Income/Expenses: tipo de operación ("Income" o "Expenses").
- Category: categoría del gasto (en varios idiomas y con alta granularidad).
- Memo: descripción libre del gasto.
- Amount: importe en euros (negativo = gasto, positivo = ingreso/compartición).

Hallazgos clave en la exploración
---------------------------------
- No hay valores nulos.
- Hay 1 registro duplicado.
- Las fechas son coherentes y están dentro del rango esperado (2021-09-30 a 2025-11-29).
- La mayoría de las transacciones (94 %) son gastos; solo un 6 % son ingresos por reparto de costes.
- Existen 48 categorías originales (mezcla de catalán, castellano e inglés), lo que dificulta el análisis.
- El importe más alto (505 €, etiquetado como "Salary") se identificó como un regalo y fue eliminado por no ajustarse al propósito del registro (gastos y repartos).
- Cuatro gastos puntuales muy elevados (compra y reparación del coche, y un máster) representan casi la mitad del gasto total acumulado.

Limpieza realizada
------------------
- Se corrigió el tipo de dato de la columna "Date" a datetime.
- Se eliminó el registro duplicado.
- Se eliminaron registros incoherentes: 
    • El "Income" de 505 € ("Salary").
    • Los registros de "Blablacar" (ya que el historial completo se gestiona en otra fuente).
    • El ingreso por promoción bancaria ("Banc Sabadell").
    • Los gastos de inversión en Salou.
- Se reetiquetó "Bizum" (como "Gasolina compartida") cuando correspondía a reparto de combustible.
- Se agruparon las 48 categorías originales en 11 categorías estandarizadas en español (p. ej.: "Alimentación", "Coche", "Ocio y Entretenimiento", etc.).
- Se procesó el campo "Memo" separando los textos por puntos para facilitar análisis posteriores.

Visualizaciones y análisis descriptivo
--------------------------------------
- Se analizó la distribución de gastos por categoría: 
    • El 67 % del gasto total corresponde a "Coche" (incluyendo compra, gasolina, reparaciones, etc.).
    • Le siguen "Alimentación" (13 %), "Ocio y Entretenimiento" (7 %) y "Regalos y Donaciones" (4 %).
- Se estudió la evolución mensual del gasto: 
    • Sin los gastos puntuales, el gasto mensual medio es de ~534 €, con variabilidad estacional (ligero aumento en invierno).
    • Se identificaron gastos recurrentes: seguro del coche (enero), revisiones (cada 6 meses), regalos (Navidad, julio, febrero).
- Se exploraron las palabras más frecuentes en el campo "Memo", lo que permite detectar patrones de consumo (ej.: "Feina", "Café", "Gasolina", etc.).

Conclusión
----------
El análisis confirma que las finanzas personales del usuario están fuertemente influenciadas por el uso del coche (especialmente la compra del vehículo en 2023). El resto de los gastos siguen patrones típicos de gasto diario y estacional. La limpieza y agrupación de categorías permiten ahora un seguimiento más claro y útil de los hábitos de consumo.

--- 

Fin del README.