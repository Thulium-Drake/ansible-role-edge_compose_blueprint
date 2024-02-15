# Compose Red Hat Device Edge blueprints from components
This role will compose blueprints for use by osbuild-composer and the Kickstart profile needed to install it.

In order to function it requires a companion repository that contains the following structure:

```
.
├── base  # contains boilerplate base blueprints for osbuild-composer
│   ├── base_jinja.toml.j2
│   └── base.toml
├── config  # Contains different config profiles which can be packaged into <image>-config.rpm
│   └── demo
│       └── etc
│           └── sample_file
├── kickstart
│   └── microshift-single-disk.ks.j2
├── modules  # Add-on modules to be incorporated in the resulting blueprint
│   ├── mod_development.toml
│   ├── mod_microshift_images.toml
│   ├── profile_demo.toml  # profiles are just like other modules, but can contain conflicting information
│   └── profile_demo.toml.j2
└── README.md
```

After generating the blueprints, they can be imported to a system prepared with https://github.com/Thulium-Drake/ansible-role-edge_image_builder
