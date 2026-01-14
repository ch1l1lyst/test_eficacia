# 📊 Dashboard Comercial - Proceso de Implementación

## 🚀 Paso a Paso: Cómo Construí el Dashboard

### **PRIMER PASO: Preparación Inicial en Excel**

Antes de nada, trabajé directamente en Excel para organizar los datos:

1. **Convertí los datos en tablas** y les puse nombres específicos para identificarlas fácilmente
    
2. **Eliminé los clientes registrados como `#N/D`** porque esos valores no servían para el análisis
    
3. **Encontré muchos datos repetidos** pero como no tenía permiso explícito para eliminarlos, los dejé tal cual
    
4. **Ajusté el formato de varias columnas** para que fueran más fáciles de analizar
    
5. **Uní los archivos de diferentes años** porque necesitaba hacer un análisis histórico de las ventas
    

**Problema encontrado:**  
Los datos con `#N/D` no se podían importar a Power BI, así que tuve que limpiarlos primero en Excel.

---

### **SEGUNDO PASO: Optimización en Power BI**

Ya en Power BI, eliminé columnas que no eran necesarias para hacer todo más rápido:

**Columnas que quité:**

- `Nro Identificacion Vendedor` → Ya tenía el nombre del vendedor
    
- `Numero de Documento` → No era relevante para mi análisis
    

**Columna que conservé:**

- `RUC Cliente` → **¡Casi la elimino!** pero me di cuenta que la necesitaba para contar clientes únicos
    

---

### **TERCER PASO: Entendiendo lo que Necesitaba**

Leí el documento con los objetivos y entendí que lo principal era:

**Agrupar los centros de costo en canales lógicos:**

- **Detallista** = Autoventa + Preventa
    
- **Autoservicios** = Todos los autoservicios unificados
    
- **Mayorista** = Solo los mayoristas
    
- **Otros** = Todo lo demás
    

---

### **CUARTO PASO: Creando la Columna "Canal"**

Creé una columna nueva en Power BI con este código:

`dax

Canal =
SWITCH(
    TRUE(),
    CONTAINSSTRING(UPPER([Centro Costo]), "AUTOVENTA"), "Detallista",
    CONTAINSSTRING(UPPER([Centro Costo]), "PREVENTA"), "Detallista",
    CONTAINSSTRING(UPPER([Centro Costo]), "AUTOSERV"), "Autoservicios",
    CONTAINSSTRING(UPPER([Centro Costo]), "MAYORISTA"), "Mayorista",
    "Otros"
)`

**¿Qué hace este código?**

- Busca "AUTOVENTA" en el centro de costo → lo pone como "Detallista"
    
- Busca "PREVENTA" → también "Detallista"
    
- Busca "AUTOSERV" → "Autoservicios"
    
- Busca "MAYORISTA" → "Mayorista"
    
- Todo lo demás → "Otros"
    

Así pude agrupar todo rápidamente y crear los gráficos.

---

### **QUINTO PASO: Organizando las Fechas**

Tenía una columna de `Año` y otra de `Mes` (en texto), pero necesitaba una fecha completa:

1. **Creé una columna `Num_Mes`** que convierte "Enero" en 1, "Febrero" en 2, etc.
    
2. **Luego creé la columna `Fecha`** combinando el año, el número del mes y el día 1
    

Ahora podía hacer análisis por fecha de verdad.

---

### **SEXTO PASO: Creando los Gráficos**

Finalmente, con todo listo, creé:

1. **Gráficos de ventas por canal** → Para ver cuál canal vende más
    
2. **Gráficos de tendencia mensual** → Para ver cómo cambian las ventas mes a mes
    
3. **Gráficos de participación** → Para ver qué porcentaje del total vende cada canal
    
4. **Tarjetas con clientes únicos** → Para contar cuántos clientes diferentes hay por canal
    

**Y así terminé el dashboard completo.**
