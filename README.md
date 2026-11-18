He preparado la primera versión funcional del Cudex OTC Financial Analytics MVP (v0.1).

Proyecto generado

v0.1

Incluye la aplicación, backend Node.js, esquema SQLite, interfaz web y un JSON de ejemplo basado en el reporte OTC que compartiste.

Descargar Cudex OTC MVP (.zip)

### Funcionalidades implementadas

| Módulo         | Funcionalidad                                   |
| -------------- | ----------------------------------------------- |
| Dashboard      | Caja USD, wallet USDT y resumen de operaciones  |
| Inversionistas | Crear y editar datos de contacto y rendimiento  |
| Ciclos         | Apertura y cierre de ciclos                     |
| Aportes        | Registro de lotes individuales                  |
| FIFO           | Asignación cronológica de capital a compras BUY |
| Rendimientos   | Cálculo único por inversionista al cierre       |
| Recuperaciones | Registro de capital devuelto y salida de caja   |
| Importaciones  | JSON con control de duplicados                  |
| Operaciones    | Historial BUY/SELL                              |
| SQLite         | Persistencia local                              |

### Reglas financieras incorporadas

* BUY: disminuye caja USD y aumenta wallet USDT.

* SELL: aumenta caja USD y disminuye wallet USDT.

* FIFO consume los lotes más antiguos.

* El porcentaje individual se conserva como una fotografía histórica en cada asignación.

* El rendimiento se genera una sola vez por inversionista y ciclo.

* No se permite cerrar un ciclo mientras existan compras elegibles con USD sin asignar.

* La recuperación de capital no reutiliza automáticamente el lote original.

### Cómo ejecutarlo

Necesitas Node.js 20 o superior.

```bash
unzip cudex-otc-mvp.zip
cd cudex-otc-mvp

npm install
npm start
```

Abre:

`http://127.0.0.1:3030`

La base de datos se crea automáticamente en `data/cudex-otc.sqlite`.

### Orden recomendado para la primera prueba

* Crear los inversionistas.

* Abrir un ciclo con la fecha correcta.

* Registrar los aportes de cada inversionista.

* Importar `examples/otc-orders-report.json`.

* Ejecutar la asignación FIFO.

* Revisar las asignaciones y el capital no financiado.

* Cerrar el ciclo y comprobar los rendimientos.

Importante: no he importado automáticamente el Excel histórico ni el JSON. El JSON está incluido como ejemplo para que puedas probar la importación. Tampoco he ejecutado una prueba integral con las dependencias instaladas; sí he comprobado la sintaxis JavaScript y la creación del esquema SQLite.

### Próxima fase

Antes de utilizarlo con dinero real, recomiendo desarrollar tres componentes:

* Conciliación del balance histórico con el Excel original.

* Auditoría de cada movimiento y posibilidad de reversión controlada.

* Copias de seguridad y restauración de SQLite.

La prioridad debe ser verificar que el saldo de caja, wallet, capital comprometido y rendimientos coincidan con tus registros reales.
