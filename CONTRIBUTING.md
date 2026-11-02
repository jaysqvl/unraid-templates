# Contributing

This repository follows the structure of the official
[Unraid Community Apps starter](https://github.com/unraid/unraid-community-apps-starter).
Use the same conventions for each application added here.

## Repository layout

| Path | Purpose |
| --- | --- |
| `templates/<app>.xml` | One version 2 Docker template per installation option |
| `docs/apps/<app>.md` | Application requirements, configuration, storage, and support |
| `icons/<app>.png` or `icons/<app>.svg` | Application artwork, when hosted here |
| `icons/README.md` | Artwork sources and license attribution |
| `ca_profile.xml` | Repository-wide Community Applications metadata |
| `icon.svg` | Repository icon |
| `README.md` | Application catalog and shared installation instructions |

Use lowercase, hyphen-separated filenames. Add a suffix such as `-cpu` or
`-nvidia` when an application needs distinct installation options. Keep all
variants in one application guide.

## Adding or updating an application

1. Confirm the container image's documented ports, volumes, environment
   variables, supported architectures, and hardware requirements.
2. Add or update the XML under `templates/`. An existing template can provide
   the XML structure; replace its application-specific settings and metadata.
3. Add an application guide under `docs/apps/` and link it from the README
   catalog. Cover first-run setup, persistent storage, updates, and support.
4. Add artwork only when its license permits redistribution, and record its
   source and license in `icons/README.md`. Preserve required license notices.
5. Validate the XML and test the installation on Unraid before requesting review.
   Include the image tag, Unraid version, hardware, and checks performed in the
   pull request. State any checks that remain outstanding.

## Template conventions

- Use `<Container version="2">` with a clear, unique `<Name>` and a valid
  `<Repository>` image reference. Use the application's supported release tag.
- Include a concise `<Overview>`, an appropriate `<Category>`, and accurate
  `<Requires>` hardware or plugin requirements.
- Set `<Project>` to the application homepage and `<Support>` to its support
  destination. Set `<ReadMe>` to the raw URL of its guide under `docs/apps/`.
- Set `<TemplateURL>` to the canonical raw URL for that exact XML file:
  `https://raw.githubusercontent.com/jaysqvl/unraid-templates/main/templates/<app>.xml`.
- Use public, stable URLs for icons and screenshots. Keep the repository
  profile and icon independent of any individual application.
- Give each configurable port, path, and variable a useful label and
  description. Keep routine settings visible and advanced settings under
  `Display="advanced"`.
- Use portable host paths, normally `/mnt/user/appdata/<app>`, with separate
  defaults for independent variants. Document every persistent mount.
- Set user/group IDs only when the image supports them. Avoid host-specific
  paths, GPU IDs, addresses, credentials, and unnecessary privileges.
- Preserve published XML paths, template names, and storage defaults when
  possible. Explain migration steps when a change affects existing installs.

Image updates and template updates are separate. An image tag can advance
without changing the XML. Template changes do not migrate existing data or
guarantee that a user's saved container settings will change.

## Validation

From the repository root, run this syntax check with Python 3. It uses only the
standard library and is also run by GitHub Actions:

```sh
python3 - <<'PY'
from pathlib import Path
import xml.etree.ElementTree as ET

for path in [Path("ca_profile.xml"), Path("icon.svg"), *sorted(Path("templates").glob("*.xml"))]:
    ET.parse(path)
    print(f"Valid XML: {path}")
PY
```

This checks XML syntax. Also verify the metadata, linked assets, default
configuration, first-run setup, and persistence after recreating the container.
For meaningful XML changes, run **Validate** and then **Scan** in the
[Community Applications submission portal](https://ca.unraid.net/submit/new).

References: [repository XML format](https://ca.unraid.net/submit/help/repository-xml),
[XML field reference](https://ca.unraid.net/submit/help/xml-field-reference),
and [repository profile](https://ca.unraid.net/submit/help/repository-info-xml).

## Catalog submission

Publishing files to GitHub does not list an application in Community Applications.
For the initial submission, sign in at the submission portal and enter
`https://github.com/jaysqvl/unraid-templates` as the repository URL. Run
**Validate** and **Scan**, review the listing previews and resolve findings,
then submit the repository for review. Follow the portal's
[submission requirements](https://ca.unraid.net/submit/help) for subsequent changes.
