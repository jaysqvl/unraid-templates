# Unraid Templates

Docker application templates for [Unraid Community Applications](https://ca.unraid.net/),
maintained by [jaysqvl](https://github.com/jaysqvl).

## Applications

| Application | Description | Templates | Setup guide |
| --- | --- | --- | --- |
| [Jotist](https://github.com/jaysqvl/Jotist) | Audio transcription, speaker labels, and notes | [CPU](templates/jotist-cpu.xml) · [NVIDIA](templates/jotist-nvidia.xml) | [Jotist on Unraid](docs/apps/jotist.md) |

## Installation

For applications listed in Community Applications, search the **Apps** tab on
your Unraid server. Choose the appropriate template, review its settings, and
follow the application's setup guide above.

### Manual installation

Templates can also be installed before they are listed in Community Applications:

1. Open a template from the table above and download its **Raw** XML file.
2. Copy it to `/boot/config/plugins/dockerMan/templates-user/` on your Unraid
   server, using a filename that does not replace an existing saved template.
3. Open **Docker → Add Container** and select it from the **Template** dropdown.
4. Review the host ports, storage paths, and application requirements, then apply.

## Support

Report template issues, such as incorrect defaults or missing settings, in
[this repository](https://github.com/jaysqvl/unraid-templates/issues). Include
the template name, Unraid version, and relevant settings or logs, with secrets
and personal information removed.

For application bugs and usage questions, use the support links in the
application's setup guide or template.

## Adding a template

See [CONTRIBUTING.md](CONTRIBUTING.md) for the repository layout, template
conventions, validation, and Community Applications submission process.

## License

Templates and documentation are [MIT licensed](LICENSE). Application images,
models, and other dependencies retain their own licenses. See
[icon attribution](icons/README.md) for artwork included in this repository.
