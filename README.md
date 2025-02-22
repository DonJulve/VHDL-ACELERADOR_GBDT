# Acelerador para árboles GBDT en VHDL

## Descripción
ste proyecto implementa un acelerador de árboles GBDT (Gradient Boosted Decision Trees) en VHDL. El diseño recibe una entrada de 8x16 bits y ejecuta los árboles almacenados en una memoria ROM, generando la salida correspondiente.

El formato de los nodos de los árboles es el siguiente:
- Nodos rama:
    - Tipo de nodo: bit 15
    - Entrada a comparar: bits 14-12
    - Desplazamiento para nodo sucesor derecho: bits 11-8
    - Valor de comparación: bits 7-0

- Nodos hoja:
    - Tipo de nodo: bit 15
    - Desplazamiento para siguiente árbol: bits 11-8
    - Salida del árbol: bits 7-0

Cuando el campo de desplazamiento toma el valor 1111, indica que es el último nodo a procesar.

El diseño incluye una señal start para indicar el inicio del procesamiento de una nueva entrada y una señal done que indica que la operación ha finalizado.

## Características
- Implementación en **VHDL**.
- Uso de **memoria ROM** para almacenar los árboles.
- Procesamiento secuencial de los nodos.
- Señales de control (start y done) para gestionar el flujo de ejecución.
- Componentes básicos: registros, multiplexor, memoria ROM y una unidad de control.

## Archivos del Proyecto
- `GBDT_incompleto.vhd`: Esqueleto original de la solución con los componentes básicos (ya resuelto).
- `gbdt_test.vhd`: Banco de pruebas para verificar el correcto funcionamiento del diseño.
- `memoriaROM_128x16.vhd`: Implementación de la memoria ROM con los árboles almacenados.
- `mux.vhd`: Implementación del multiplexor.
- `reg.vhd`: Implementación de los registros.

## Requisitos
Para simular y sintetizar el diseño se necesita:
### Linux:
- **GHDL** para simulación.
- **GTKWave** para visualizar las señales.
### Windows:
- **Modelsim** para simular y visualizar.

## Instalación y Uso
1. Clona el repositorio:
   ```sh
   git clone https://github.com/DonJulve/VHDL-ACELERADOR_GBDT.git
   cd VHDL-ACELERADOR_GBDT
   ```
2. Ejecuta la simulación con GHDL:
   ```sh
   ghdl -a -fsynopsys -fexplicit *.vhd
   ghdl -e -fsynopsys -fexplicit testbench
   ghdl -r -fsynopsys -fexplicit testbench --vcd=output.vcd --ieee-asserts=disable --stop-time=500ns

   ```
3. Visualiza la salida con GTKWave:
   ```sh
   gtkwave output.vcd
   ```
