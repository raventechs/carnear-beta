# carnear-beta — Proyecto Training Wheels (piloto: CarneAR)

Una sola app con dos modos, solo por habilitación:

- **Principiante** (cliente nuevo): pantalla única para cobrar un importe + medio de pago, pestaña "Hoy" y "Más" (cierre de caja, backup, pedir la versión completa). Sin catálogo, stock ni sucursales.
- **Avanzado** (todo lo anterior): catálogo, venta por kilos, stock, gastos, proveedores, sucursales. Al pasar, carga inicial guiada del catálogo y ajuste de precios en bloque (con vista previa y deshacer).

## Cómo funciona
- Campo `modo` en `clientes/{email}` (`principiante` | `avanzado`). Sin campo = Avanzado (cuentas anteriores no cambian).
- El cliente nuevo se crea como `principiante`. Solo el admin cambia el modo (menú oculto → Mis clientes → botón).
- Las ventas y datos son los mismos en ambos modos: pasar de uno a otro no migra ni borra nada.
- Admin: en Config (arriba) hay "Ver mi app como…" con 3 vistas, solo en su teléfono y solo con su cuenta: Completo con sucursales (panel de sus locales), Completo común (un solo local, como lo ve un cliente) y Principiante. También está en el menú oculto (5 toques al logo).

## Reglas Firestore
Ver `qa/rules/carnear-fase3.rules` en el repo `gasar`: agrega `modo` (solo `principiante`) a la alta del cliente. Si todavía no están publicadas, la app crea la cuenta sin `modo` y queda como Avanzado.

## v2.9-tw2 — cómo el cliente descubre la versión completa (sin asustarse)
- Aviso suave en Cobrar tras 10 ventas o 7 días de uso (se pospone 7 días con "Ahora no").
- En Más: lista con candados (catálogo y kilos, stock, gastos y proveedores, varias sucursales); cada una con "Quiero esto" que avisa por WhatsApp con el tema.
- Panel admin: por cada cliente Principiante, ventas y días de uso, con aviso "momento de ofrecerle la completa".

Versión: v2.9-tw2 = producción v2.7 + venta por kilos (beta v2.8) + Training Wheels.
