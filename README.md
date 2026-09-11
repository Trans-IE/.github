# .github

Archivos por defecto de la organización. GitHub aplica lo que hay acá a **todos los repos
de Trans-IE que no tengan su propia versión** — un repo con su propio
`pull_request_template.md` usa el suyo y este se ignora.

El nombre del repo tiene que ser exactamente `.github`: es el único que GitHub reconoce
para esto.

| Archivo | Efecto |
|---|---|
| `.github/pull_request_template.md` | Precarga el cuerpo de todo PR nuevo de la organización |

## Por qué importa el template

La sección **"Qué cambia"**, entre los marcadores `<!-- release-notes:start -->` y
`<!-- release-notes:end -->`, no es decorativa: es el texto que se publica **tal cual** en
las release notes. El workflow de release lo cosecha de cada PR del rango en vez de usar
el título, que GitHub autogenera desde el nombre de rama y queda inservible
("Development", "Fix/teams list").

El workflow `pr-lint` de [Trans-IE/gh-workflows](https://github.com/Trans-IE/gh-workflows)
bloquea el PR si esa sección no tiene al menos un bullet. Así que editar este archivo
cambia lo que se le pide a la gente en todos los repos a la vez — conviene pensarlo dos
veces.

Los checkboxes de "Requerimientos de despliegue" también se leen: generan un aviso
destacado arriba del release cuando la versión necesita una migración.

## Cuidado al editar

Esto **no está versionado**. A diferencia de los reusable workflows, que se consumen por
tag (`@v1`), los archivos por defecto se leen siempre de la rama por defecto de este repo.
Un cambio acá impacta en el próximo PR de cualquier repo, sin intermediarios.

Si movés o renombrás los marcadores de release notes, el cosechador deja de encontrarlos y
cae al título del PR. Los marcadores y el heading "Qué cambia" son la interfaz con
`release-notes.sh`.
