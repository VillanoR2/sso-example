# Pruebas unitarias para IdP (SSO mini)

Esta carpeta contiene pruebas unitarias para los módulos del IdP minimalista implementado en `idp/`.

Estructura relevante

- `idp/config.js` — configuración y constantes.
- `idp/storage.js` — funciones: `buscarUsuarioPorEmail`, `guardarCodigo`, `consumirCodigo`, `limpiarCodigosExpirados`.
- `idp/tokenService.js` — función: `crearTokenAcceso`.
- `idp/routes.js` — router con endpoints `/login`, `/authorize`, `/token`, `/me`.
- `tests/idp/` — pruebas unitarias y de integración para los módulos anteriores.

Cómo ejecutar las pruebas (Windows / PowerShell)

1) Instala dependencias (ya incluidas en este repo):

```powershell
npm install
```

2) Ejecuta el runner de tests de Node.js (incluye `node:test`):

```powershell
node --test
```

Esto ejecutará los tests en `tests/idp/*.test.js`.

Descripción rápida de los tests

- `config.test.js`: valida que las constantes exportadas están definidas y tienen el tipo esperado.
- `storage.test.js`: pruebas unitarias de almacenamiento en memoria (buscar usuario, guardar/consumir códigos, limpieza).
- `tokenService.test.js`: genera un JWT y verifica su firma y claims usando `jose`.
- `routes.test.js`: prueba de integración ligera que monta el router en una app Express con `express-session` y usa `supertest` para simular el flujo `/login` → `/authorize` → `/token`.

Notas

- Estas pruebas usan `supertest` para probar las rutas de Express; `supertest` está instalado como dependencia de desarrollo.
- Las pruebas están diseñadas para entornos locales y educativos; no son pruebas de seguridad o de producción.

Si quieres un script npm para ejecutar las pruebas, puedo agregar en `package.json` un script `test:unit` que haga `node --test`.
