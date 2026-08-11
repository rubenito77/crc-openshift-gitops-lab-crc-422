# CRC OpenShift GitOps Lab - OCP 4.22

Laboratorio practico para implementar un flujo GitOps con Red Hat OpenShift
GitOps y Argo CD sobre un cluster local OpenShift creado con CRC.

## Entorno

- Microsoft Windows con PowerShell
- CRC
- OpenShift Container Platform 4.22.1
- Red Hat OpenShift GitOps 1.21.2
- Argo CD administrado por OpenShift GitOps
- Repositorio publico de GitHub

## Objetivo

Desplegar una aplicacion de ejemplo desde este repositorio Git y demostrar:

1. Renderizado de manifiestos mediante Kustomize.
2. Despliegue declarativo mediante Argo CD.
3. Sincronizacion manual inicial.
4. Sincronizacion automatica.
5. Eliminacion de recursos obsoletos con `prune`.
6. Correccion de cambios manuales con `selfHeal`.
7. Reconciliacion del estado del cluster con el estado declarado en Git.

## Aplicacion de ejemplo

| Propiedad | Valor |
| --- | --- |
| Aplicacion | `app-demo` |
| Ambiente | `dev` |
| Namespace | `gitops-demo-dev` |
| Imagen | `registry.access.redhat.com/ubi9/httpd-24:latest` |
| Puerto | `8080` |
| Exposicion | OpenShift Route |
| Registro privado | No requerido |
| Secret de imagen | No requerido |

## Estructura prevista

```text
crc-openshift-gitops-lab-crc-422/
|-- README.md
|-- apps/
|   `-- app-demo/
|       |-- base/
|       |   |-- configmap.yaml
|       |   |-- deployment.yaml
|       |   |-- service.yaml
|       |   |-- route.yaml
|       |   `-- kustomization.yaml
|       `-- overlays/
|           `-- dev/
|               `-- kustomization.yaml
`-- argocd/
    `-- app-demo-dev.yaml
```

## Flujo GitOps

```text
GitHub -> OpenShift GitOps / Argo CD -> gitops-demo-dev -> app-demo
```

Git sera la fuente de verdad. Los recursos de la aplicacion no se aplicaran
manualmente con `oc apply`; Argo CD sera responsable de crearlos y reconciliarlos.

## Estado

- [x] Cluster CRC operativo.
- [x] Red Hat OpenShift GitOps instalado.
- [x] Instancia predeterminada de Argo CD validada.
- [x] Repositorio Git creado.
- [ ] Manifiestos base de la aplicacion.
- [ ] Overlay Kustomize para desarrollo.
- [ ] Application de Argo CD.
- [ ] Primera sincronizacion manual.
- [ ] Sincronizacion automatica y prueba de reconciliacion.
