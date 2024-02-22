# Compose Red Hat Device Edge blueprints from components
This role will compose blueprints for use by osbuild-composer and the Kickstart profile needed to install it.

In order to function it requires a companion repository that contains the following structure:

```
.
├── base
│   ├── base_jinja.toml.j2
│   ├── base.toml
│   └── base.toml.j2
├── kickstart
│   └── microshift-single-disk.ks.j2
├── modules
│   ├── development
│   │   └── development.toml.j2
│   └── guestbook
│       ├── files
│       │   └── usr
│       │       └── lib
│       │           └── microshift
│       │               └── manifests.d
│       │                   └── guestbook
│       │                       ├── frontend-deployment.yaml
│       │                       ├── frontend-service.yaml
│       │                       ├── kustomization.yaml
│       │                       ├── namespace.yaml
│       │                       ├── README.md
│       │                       ├── redis-follower-deployment.yaml
│       │                       ├── redis-follower-service.yaml
│       │                       ├── redis-leader-deployment.yaml
│       │                       └── redis-leader-service.yaml
│       └── guestbook.toml
└── README.md
```

After generating the blueprints, they can be imported to a system prepared with https://github.com/Thulium-Drake/ansible-role-edge_image_builder

## Config RPM modules
This role will generate an RPM that will contain the selected configuration modules, please note that the files are copied in the order defined in the variables file. In the case of conflicting filepaths, the last file wins.

If creating a new config module, keep in mind that you need to create the whole directory structure required for the files. For example, adding a Kustomize manifest should be placed in one of the following locations:

  * /etc/microshift/manifests
  * /etc/microshift/manifests.d/*
  * /usr/lib/microshift/
  * /usr/lib/microshift/manifests.d/*

Where ```manifests.d``` contains other directories with all configuration manifest file and the ```/etc/``` tree is writeable after the image has been compiled.
