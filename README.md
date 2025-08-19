# TELECOM-X-2

2da parte trabajo telecom x alura challenge

###INFORME###

En este informe se destacan los factores clave que influyen en la evasión de clientes —como el tipo de contrato, el gasto mensual, la falta de servicios de soporte y el método de pago— y se proponen estrategias concretas de retención. Además, se compara el desempeño de la Regresión Logística y del Random Forest, y se explica por qué este último resulta más efectivo para el caso de Telecom X.

##Resumen del análisis##

El conjunto de datos de Telecom X contiene 7.267 clientes con 23 variables que describen datos demográficos, servicios contratados, condiciones de facturación y métricas financieras. La variable objetivo es Churn/Churn_flag, que indica si el cliente canceló (≈ 26 %) o permaneció en la compañía (≈ 74 %). Se realizó un análisis exploratorio y un preprocesamiento exhaustivo: eliminación de columnas irrelevantes (customerID, Cuentas_Diarias, account.Charges.Total), codificación de variables categóricas mediante one‑hot encoding, normalización de variables numéricas cuando el modelo lo requería y división en conjuntos de entrenamiento y prueba (80/20) estratificados.

#Principales correlaciones encontradas#

	•	Tiempo con la empresa (MesesContrato): correlación negativa con la cancelación. Los clientes que han permanecido menos de dos años presentan una mayor probabilidad de cancelar.

	•	Gasto mensual (CargoMensual): correlación positiva moderada con la cancelación; clientes con cargos mensuales altos (especialmente > 70 unidades monetarias) tienen mayor riesgo de irse.

	•	Tipo de Internet: los usuarios de fibra óptica muestran una tasa de cancelación ~40 %, muy superior a la de los usuarios de DSL (~18 %) o de quienes no contratan internet (~7 %).

	•	Servicios de seguridad y soporte: no tener OnlineSecurity, OnlineBackup, DeviceProtection o TechSupport incrementa la cancelación a alrededor del 38–40  %; disponer de estos servicios reduce la tasa a 14–22  %.

	•	Tipo de contrato: los contratos de mes a mes tienen una tasa de cancelación muy alta (~41  %), mientras que los contratos de un año y dos años presentan tasas de cancelación mucho menores (~11  % y 3  %, respectivamente).

	•	Método de pago: el cheque electrónico es el método con mayor cancelación (~44  %), seguido del cheque físico (~18  %) y transferencia bancaria (~16  %); tarjeta de crédito exhibe la menor tasa (~15  %).

	•	Variables demográficas: los clientes sin pareja o sin dependientes tienen tasas de cancelación notablemente mayores (≈30–32  %) que quienes tienen pareja o dependientes (≈15–19  %). Los adultos mayores presentan una ligera mayor propensión a cancelar.

#Desempeño de los modelos#

Se construyeron dos modelos predictivos: una Regresión Logística con normalización de variables numéricas y un Random Forest sin normalización. Ambos utilizaron el mismo preprocesamiento de one‑hot encoding para las variables categóricas.

#Regresión Logística#

	•	Exactitud: ~0,79 en entrenamiento y ~0,78 en prueba.

	•	Precisión: ~0,65, Recall: ~0,51, F1-score: ~0,57 (valores aproximados).

	•	La cercanía entre las métricas de entrenamiento y prueba indica un buen balance; no muestra signos evidentes de sobreajuste. Sin embargo, su capacidad para detectar a todos los clientes cancelados (recall) es limitada.

	•	Variables más influyentes: las mayores magnitudes de los coeficientes se asociaron con account.Contract_Month-to-month, internet.InternetService_Fiber optic, ausencia de servicios de soporte y seguridad (internet.TechSupport_No, internet.OnlineSecurity_No), el método de pago MetodoPago_ChequeElectronico y un CargoMensual elevado. Dichas variables incrementan notablemente la probabilidad de cancelación. En sentido contrario, customer.Partner_Yes, customer.Dependents_Yes y los contratos de Two year reducen la probabilidad de churn.

#Random Forest#

	•	Exactitud: ~0,80 en entrenamiento y ~0,79 en prueba.

	•	Precisión: ~0,69, Recall: ~0,50, F1-score: ~0,58 (valores aproximados).

	•	El desempeño entre entrenamiento y prueba es consistente, lo que sugiere ausencia de sobreajuste significativo. El modelo mejora ligeramente la exactitud y precisión respecto a la Regresión Logística.

	•	Importancia de variables: según la medida de importancia de Gini, las variables principales son MesesContrato, CargoMensual, internet.InternetService_Fiber optic, account.Contract_Month-to-month, MetodoPago_ChequeElectronico y la falta de servicios de seguridad o soporte técnico. Estas variables contribuyen de forma decisiva a las divisiones de los árboles.

Factores clave en la cancelación y estrategias de retención

Los resultados combinados del análisis exploratorio y de los modelos permiten identificar los factores que más influyen en la evasión de clientes y plantear estrategias de retención.

#Factor clave#


Duración del contrato

Tipo de Internet (fibra óptica)

Servicios de seguridad y soporte

Método de pago (cheque electrónico)

Gasto mensual elevado

Situación familiar (sin pareja/dependientes)


#EVIDENCIA#


Los contratos mes a mes tienen una probabilidad de cancelación muy superior a los contratos de uno o dos años.

La fibra óptica presenta la mayor tasa de churn (~40 %).

La ausencia de OnlineSecurity, OnlineBackup, DeviceProtection o TechSupport incrementa la cancelación.

El cheque electrónico está asociado a la cancelación más alta (~44  %).

Los clientes con cargos mensuales altos son más propensos a cancelar.

La ausencia de pareja o dependientes se relaciona con tasas de churn mayores (~30 %).


#Estrategia de retención recomendada#

Incentivar contratos a largo plazo mediante descuentos o beneficios (por ejemplo, meses gratis o precios preferenciales) y campañas específicas para clientes con menos de 12 meses de servicio.

Revisar la experiencia de usuario en fibra: mejorar la calidad del servicio, ofrecer paquetes premium con soporte 24 horas y migrar clientes de DSL a fibra con ofertas de fidelidad para evitar cancelación.

Crear paquetes que incluyan estos servicios a precios accesibles; ofrecer pruebas gratuitas o descuentos iniciales para incentivar su contratación; educar a los clientes sobre los beneficios de protección y soporte técnico.

Promocionar métodos de pago automáticos como tarjeta de crédito o transferencia, tal vez ofreciendo incentivos (descuentos por domiciliación) y simplificando el proceso de cambio de medio de pago.

Revisar la estructura tarifaria: ofrecer planes escalonados o descuentos por consumo; contactar de forma proactiva a los clientes con cargos altos para ofrecer paquetes adaptados a sus necesidades.

Diseñar campañas de fidelización personalizadas para clientes solteros, brindando ofertas que refuercen el valor del servicio (por ejemplo, paquetes de entretenimiento).


#Recomendaciones generales#


	1.	Segmentación de clientes de alto riesgo: utilizar el modelo (preferiblemente el Random Forest, dado su mejor desempeño) para predecir el riesgo de cancelación y generar listas de clientes prioritarios para acciones preventivas.

	2.	Programas de fidelización temprana: concentrar esfuerzos en clientes con MesesContrato bajos (menos de 12), ofreciéndoles beneficios por mantener el servicio y persuadiéndolos a migrar a contratos de largo plazo.

	3.	Mejora de la experiencia en servicios de fibra óptica: invertir en infraestructura y atención al cliente para reducir quejas y fallos, ya que este segmento presenta altos niveles de churn.

	4.	Paquetes de valor agregado: promover servicios de seguridad, backup y soporte técnico como elementos diferenciadores que disminuyen la evasión.

	5.	Optimización de métodos de pago: incentivar el pago por tarjeta o transferencia, eliminando o encareciendo gradualmente la opción de cheque electrónico, ya que se asocia con altas tasas de cancelación.

	6.	Monitorización continua y actualización del modelo: dado que los patrones de comportamiento pueden cambiar con el tiempo, actualizar periódicamente el modelo con datos recientes y evaluar otras técnicas (por ejemplo, boosting o redes neuronales) para mejorar el recall y reducir falsos negativos.


#En conclusión#

 
 La cancelación de clientes en Telecom X está fuertemente influenciada por la duración del contrato, el tipo de servicio de internet, la contratación de servicios de protección/soporte y el método de pago. La combinación de análisis exploratorio y modelos predictivos permite no solo anticipar qué clientes corren mayor riesgo de cancelar, sino también diseñar estrategias de retención específicas que mejoren la fidelización y reduzcan la pérdida de ingresos.
