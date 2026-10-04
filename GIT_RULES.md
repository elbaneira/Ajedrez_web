# Reglas Git del proyecto

1. NUNCA hacer `git push` (ni a origin ni a ningún remoto).
2. SIEMPRE leer este archivo (`GIT_RULES.md`) antes de ejecutar cualquier comando relacionado con `.git` (`init`, `add`, `commit`, `status`, `log`, `remote`, etc.).
3. Los commits son solo locales.
4. No configurar ni usar remotos sin permiso explícito del usuario.
5. NUNCA subir información sensible: tokens, PATs, contraseñas, claves API, archivos `.env`, credenciales, certificados (`*.pem`, `*.key`, `*.pfx`), ni datos personales. Si algo sensible llega al repo, avisar y rotarlo de inmediato.
6. Todo lo listado en `.gitignore` queda fuera de `git add` / commits.
