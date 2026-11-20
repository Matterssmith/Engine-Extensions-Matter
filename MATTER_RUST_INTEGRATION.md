# Telegram-Matter — conector Rust de Matter-Rust

**Estado:** contrato definido; no hay conexión Telegram activa ni token configurado.

- Motor compartido: `Matterssmith/Base-Matter`, rama `feat/matter-rust-multiplatform`, crate `crates/matter-rust`.
- Transporte Telegram: implementar con **teloxide 0.17.0** (Rust) como opción revisada; usar **Bot API** y autenticación de bot con token en gestor de secretos del servidor, nunca en GitHub.
- Eventos: normalizar `chat_id`, `from.id`, `message_id`, edición, canal/foro, media, comandos, callbacks y botones nativos, conservando IDs Telegram propios y sin aplicar JID WhatsApp.
- Interactividad: teclado inline y callback queries Telegram NO equivalen a NativeFlow WhatsApp; crear representaciones por capacidades disponibles.
- Seguridad: validar token servidor, longitud/formatos, nonces de callback cuando apliquen, protección de duplicados persistente, rate limits y controles de privacidad. `username` es alias mutable, NO identidad de owner global.
- Vault es autoridad separada de permisos; Matter-Rust no concede rangos por contenido de mensajes.
- Mantener modo deshabilitado hasta E2E y revisión. No compartir sesiones o credenciales WhatsApp.
- Actualizaciones: revisar versiones oficiales teloxide y Telegram Bot API, diffs y breakages, actualizar README/continuidad, ejecutar tests Linux/Windows y luego E2E, pin de versión y rollback.

Pendiente: implementar adapter real, webhook/polling, almacenamiento secreto y autenticación de ingreso. El crate común actualmente solo tiene pruebas offline.

Créditos:
Hecho por Lournyx Matterssmith [Lou-Nyx].
