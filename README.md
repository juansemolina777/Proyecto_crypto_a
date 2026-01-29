Proyecto de Criptomonedas (Qlik Sense)

Panel de análisis del mercado cripto con Qlik Sense, modelo estrella y SQL.

Este proyecto es un análisis de las principales criptomonedas a partir de datos históricos obtenidos vía API, con modelado en esquema estrella y visualización en Qlik Sense.

El objetivo principal es responder preguntas como:

💡 “¿Cómo se comportan las principales criptomonedas en el tiempo y qué tan atractivo es cada activo según rendimiento y volatilidad?”

🧾 Conjunto de datos

Fuente: API pública de criptomonedas (por ejemplo CoinGecko / Binance).

Período: ejemplo 01/01/2020 – 31/12/2023.

Obtención: Llamados a API + export a CSV.

Archivo: data/crypto_prices.csv

Campos principales:

symbol – Símbolo de la cripto (BTC, ETH, ADA, etc.).

name – Nombre del activo.

date – Fecha.

price_open – Precio de apertura.

price_close – Precio de cierre.

price_high – Máximo diario.

price_low – Mínimo diario.

volume – Volumen operado.

market_cap – Capitalización de mercado.

dominance – Dominancia de la cripto vs. mercado total (opcional).

🧱 Modelado: esquema estrella

Para facilitar el análisis se construyó un modelo estrella con:

Tabla de hechos: Fact_CryptoPrices

crypto_id

date_id

price_open

price_close

price_high

price_low

volume

market_cap

return_daily (variación % diaria)

volatility_30d (volatilidad móvil a 30 días, calculada en el modelo)

Dimensiones:

Dim_Crypto

crypto_id

symbol

name

category (Layer 1, DeFi, Stablecoin, etc.)

launch_year

Dim_Date

date_id

date

day / month / year

quarter

is_weekend

El modelo permite:

Comparar fácilmente activos entre sí.

Analizar comportamiento por períodos (años, meses, ciclos de mercado).

Medir rendimiento y riesgo (volatilidad) por cripto.

📎 El diagrama del modelo se puede ver en:
img/modelo_estrella_crypto.png

🔁 Proceso ETL (resumen)

Antes de llegar al tablero, se realizó:

Llamados a API de criptomonedas y consolidación en un histórico.

Limpieza de datos (fechas, símbolos, duplicados).

Conversión de tipos numéricos (precios, volumen, market cap).

Creación de crypto_id y date_id para el modelo estrella.

Cálculo de métricas derivadas:

return_daily

retornos acumulados por activo

volatilidad móvil (por ventana de n días).

Carga del modelo en Qlik Sense usando tablas RESIDENT y joins controlados.

📊 Panel de control en Qlik Sense

El archivo del proyecto está en:

qlik/Crypto_Analytics.qvf

Principales elementos del tablero

KPIs iniciales:

Rendimiento acumulado BTC vs. resto del mercado.

Criptomoneda con mejor performance en el período seleccionado.

Volatilidad promedio (30 días) del top de activos.

Market cap total del mercado.

Dominancia de BTC / ETH.

Gráficos y tablas:

Evolución de precio y volumen por criptomoneda (líneas + columnas).

Comparación de rendimiento acumulado entre varios activos (BTC, ETH, etc.).

Mapa de calor de volatilidad por cripto y período.

Ranking de criptomonedas por:

rendimiento

volatilidad

relación retorno/riesgo

Distribución del market cap por categoría (Layer 1, DeFi, Stablecoins…).

📎 Algunas capturas del tablero se encuentran en img/crypto_dashboard_*.png.

🎨 Diseño y UX

El tablero se diseñó con un enfoque:

Fondo oscuro tipo terminal / trading.

Paleta basada en:

Verdes para rendimiento positivo.

Rojos para caídas.

Azules para métricas neutras o de contexto.

KPIs claros en la parte superior, agrupados en:

Visión general del mercado.

Rendimiento.

Riesgo / volatilidad.

Navegación por pestañas / hojas:

Overview (visión general).

Rendimiento por activo.

Riesgo y volatilidad.

Comparación de activos.

La idea fue lograr un tablero que pueda usar tanto alguien de negocio como alguien más técnico que mira mercado todos los días.

🚀 Cómo abrir el proyecto

Descargar el archivo:
qlik/Crypto_Analytics.qvf

Abrirlo con Qlik Sense Desktop.

Revisar:

El modelo de datos (diagram view).

Las hojas de análisis con los gráficos y KPIs.

💭 Ideas de uso

Este proyecto puede servir como ejemplo de:

Cómo aplicar modelo estrella a datos de mercado financiero / cripto.

Proceso ETL básico desde una API a un modelo analítico.

Construcción de dashboards en Qlik Sense enfocados en:

rendimiento

riesgo

comparación entre activos.

Material para portfolio, entrevistas o publicaciones en LinkedIn sobre análisis de datos financieros.

📬 Contacto

Si te interesa ver más detalles del proceso (scripts de carga, consultas, métricas calculadas, etc.) o tenés feedback, ¡bienvenido! 🙂

Podés escribirme a juansemolinaok5@gmail.com
 o por LinkedIn:
linkedin.com/in/juanse-molina-2354501ba
