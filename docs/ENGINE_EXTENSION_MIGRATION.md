# Telegram-Matter → Engine-Extensions-Matter: migración controlada

Fecha: 2026-11-23. Estado: **fase de preparación documental, sin cambios de runtime**.

## Responsabilidad definitiva

Engine-Extensions-Matter será el único proyecto responsable de los adaptadores de terceros para WhatsApp, Telegram, Discord y futuras redes. Se comunica con Engine-Matter mediante contratos versionados; jamás introduce implementaciones de redes externas en el núcleo. Engine-Matter aloja la integración Matter-MSEL y los sistemas Matter propios, incluido Social-Matter. MSEL, lenguaje oficial, permanece en Matterssmith/MSEL; la carpeta `Matter-MSEL/` se aloja en Engine-Matter, no aquí.

Engine-Extensions-Matter no es **Extensions-Matter**, repositorio privado existente para otros módulos/Anti; mantener ambos aislados y conservar sus historiales.

## Estructura de destino

- `adapters/whatsapp/`: portar desde WhatsApp-Matter/alpha `providers/whatsapp-rust/`, `providers/baileys/`, `providers/whatsmeow/`, `crates/whatsapp-contracts/`, bindings y templates tras auditoría; no copiar sesiones ni secretos.
- `adapters/telegram/`: contrato y proveedor Telegram cuando se implemente y pruebe.
- `adapters/discord/`: contrato y proveedor Discord solo tras rescatar cualquier código útil antes del retiro del repositorio antiguo.
- `contracts/`: contratos públicos de evento, salida, plataforma, identidad de sesión y capacidad, sin conceder autoridad por datos del mensaje.

## Orden y condiciones de corte

1. Inventariar y fijar SHAs de repositorios origen, CI, referencias Cargo/Go/JS/TS, links y configuraciones externas; conservar respaldo verificable del historial Git.
2. Diseñar ABI y contratos versionados Engine↔Extension: entrada sin confianza, autenticación del transporte, anti-replay, consentimiento, scope de sesión, autorización Vault, salida separada.
3. Copiar primero componentes y pruebas de WhatsApp-Matter, sin borrar el origen. No afirmar que Baileys o whatsmeow sean transportes funcionales si solo normalizan eventos.
4. Añadir Telegram y Discord por adaptadores separados y pruebas sintéticas. No habilitar ningún conector por defecto.
5. Comprobar CI Linux/Windows, ausencia de claves y de accesos privilegiados implícitos; verificar prueba real con una sola sesión ya existente antes de tocar el proveedor antiguo.
6. Tras el corte validado, retirar el código duplicado de Engine-Matter, renombrar GitHub desde una cuenta con permisos administrativos y actualizar referencias. Solo entonces plantear eliminación de Discord-Matter tras respaldo y verificación.

**Restricciones:** mantener en producción la sesión WhatsApp actual; no crear pairing ni segundo proceso con el mismo estado; no mover llaves maestras Vault, credenciales, SQLite, tokens o historiales privados. Bot-Matter continúa bloqueado.

## Validación pendiente

Los nuevos directorios son instrucciones de preparación, no adaptadores ejecutables. Quedan pendientes compilación, pruebas de integración, CI, despliegue y renombrado. Ninguna capacidad real se declara obtenida por esta documentación.

Créditos:
Hecho por Lournyx Matterssmith [Lou-Nyx].
