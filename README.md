# Unraid templates

Unraid Community Applications templates maintained by Jay Esquivel for
[Jotist](https://github.com/jaysqvl/Jotist), a self-hosted audio transcription app.

| Template | Image | Hardware |
| --- | --- | --- |
| [Jotist-CPU](templates/jotist-cpu.xml) | `ghcr.io/jaysqvl/jotist:latest` | Intel/AMD 64-bit CPU |
| [Jotist-NVIDIA](templates/jotist-nvidia.xml) | `ghcr.io/jaysqvl/jotist:latest-cuda` | Intel/AMD 64-bit CPU and a CUDA 12.6-compatible NVIDIA GPU |

Both templates track stable releases. NVIDIA requires Unraid's
[NVIDIA Driver plugin](https://forums.unraid.net/topic/98978-plugin-nvidia-driver/)
and a compatible host driver. RTX 50-series/Blackwell inference is not qualified
for the CUDA 12.6 image. CPU/GPU model support and memory requirements vary;
consult Jotist's in-app model catalog.

## Install

The templates are prepared for Community Applications submission. A public
repository alone does not make them appear in the Apps catalog.

Once listed, search the Apps tab for **Jotist-CPU** or **Jotist-NVIDIA**, choose
the appropriate option, and review its port and appdata folders before applying.
The default HTTP port is **8080**; choose another host port if it is occupied.
For NVIDIA, leave `NVIDIA_VISIBLE_DEVICES` as `all` or enter a GPU UUID from the
NVIDIA Driver settings. The template enables `--runtime=nvidia` and
`compute,utility` capabilities.

Open the container's **WebUI** to create the first account. Local transcription
runs on your server. Optional cloud transcription and LLM features send content
to the provider you configure. Models and runtime dependencies download when
needed; allow disk space for the selected models.

## Persistent storage

Each template supplies three bind mounts. Their default parent folder is
`/mnt/user/appdata/jotist-cpu` or `/mnt/user/appdata/jotist-nvidia`:

| Host subfolder | Container path | Contents |
| --- | --- | --- |
| `data` | `/app/data` | Database, recordings, transcripts, settings, and generated signing secret |
| `whisperx-env` | `/app/whisperx-env` | Managed Python environments and model files |
| `home` | `/home/appuser` | Hugging Face, Torch, and package/download caches |

Keep all three mounts when updating or recreating a container. Back up the
application data and signing secret. The app creates its signing secret on first
start and keeps it in the persistent data folder.

The advanced `PUID`/`PGID` defaults are **99:100** (Unraid's `nobody:users`).
Jotist's entrypoint starts as root to prepare permissions, then runs the app as
that user and group.

The templates use different default data folders so two installations do not
open the same database. They still need different host ports if run together.
When switching CPU/NVIDIA variants or migrating an existing installation, stop
the previous container first and carry forward its actual three mount paths,
database path, signing secret, and effective UID/GID. Follow Jotist's
[migration guide](https://github.com/jaysqvl/Jotist/blob/main/docs/jotist-migration.md).

## Updates

The templates keep the same `latest` and `latest-cuda` image references across
normal stable releases. Jotist's release process advances those tags. Unraid's
image update check can then offer the new image; installation happens when the
user chooses Update or through their configured automatic updater.

Template changes are needed when installation settings change, such as required
environment variables, mount paths, ports, or GPU setup. Existing installations
may need those settings changed in their container editor; updating the catalog
template does not migrate existing data or guarantee that saved settings change.
Users can enter a versioned image tag in the Repository field to stay on a
specific release.

## Submit this repository

1. Open the [Community Apps submission portal](https://ca.unraid.net/submit/new)
   and sign in with your Unraid account.
2. Enter **`https://github.com/jaysqvl/unraid-templates`** as the repository URL.
3. Run **Validate** and **Scan**. Confirm the preview contains **Jotist-CPU** and
   **Jotist-NVIDIA**, the correct image tags, icon, support links, and hardware
   requirements. Resolve any portal findings before proceeding.
4. Review the final submission and click **Submit** when ready.

The repository includes the required root `LICENSE`, `ca_profile.xml`, and one
version 2 Docker XML file per option. The `TemplateURL` fields point to their
canonical raw GitHub files. See the official
[submission requirements](https://ca.unraid.net/submit/help) and
[XML field reference](https://ca.unraid.net/submit/help/xml-field-reference).

## Support and licensing

- [Template installation issues](https://github.com/jaysqvl/unraid-templates/issues)
- [Jotist application issues](https://github.com/jaysqvl/Jotist/issues)
- [Jotist documentation](https://github.com/jaysqvl/Jotist#readme)

Templates and repository documentation are MIT licensed. The Jotist icon in
`icons/jotist.png` is the existing Jotist brand asset, copied without modification.
Jotist is an independently maintained continuation of Scriberr; see its
[attribution](https://github.com/jaysqvl/Jotist/blob/main/ATTRIBUTION.md) and
[MIT license](https://github.com/jaysqvl/Jotist/blob/main/LICENSE). Model and
third-party runtime licenses remain separate from these templates.
