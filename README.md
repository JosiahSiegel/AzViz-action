# AzViz (Azure Visualizer) action

![](https://badgen.net/badge/icon/gitguardian/green?icon=gitguardian&label)
[![Manually triggered full workflow](https://github.com/JosiahSiegel/AzViz-action/actions/workflows/sample_full_workflow.yml/badge.svg)](https://github.com/JosiahSiegel/AzViz-action/actions/workflows/sample_full_workflow.yml)

Donate to [AzViz Developer](https://github.com/PrateekKumarSingh/AzViz#readme)

## Synopsis

[GitHub action](https://github.com/marketplace?type=actions) ready [AzViz](https://github.com/PrateekKumarSingh/AzViz)!

## Inputs

### Required

```yml
inputs:
  resource-group:
    description: Comma-seperated resource group list
    required: true
  out-file:
    description: Graph export path
    required: true
    default: viz.png
  sub-name:
    description: Azure subscription name
    required: true
    default: Pay-As-You-Go
```

### Optional

```yml
  theme:
    description: Graph theme (dark, light, neon)
    required: false
    default: neon
  depth:
    description: Level of Azure Resource Sub-category to be included in vizualization (1 or 2)
    required: false
    default: '1'
  verbosity:
    description: Level of information to included in vizualization (1 or 2)
    required: false
    default: '1'
  format:
    description: Graph format (png or svg)
    required: false
    default: png
  direction:
    description: Direction in which resource groups are plotted on the visualization (left-to-right or top-to-bottom)
    required: false
    default: top-to-bottom
  exclude-types:
    description: Exclude resources via string search
    required: false
    default: '*excludethisthing1,excludethisthing2*'
  splines:
    description: Controls how edges appear in visualization. ('spline', 'polyline', 'curved', 'ortho', 'line')
    required: false
    default: spline
```

## Quick start

`sample_min_workflow.yml`
```yml
jobs:
  Windows-latest:
      runs-on: windows-latest
      steps:
        - name: Login to Azure
          uses: azure/login@v1
          with:
            creds: ${{ secrets.SERVICE_PRINCIPAL_CREDS }} 
            enable-AzPSSession: true
        - uses: JosiahSiegel/AzViz-action@v1
          with:
            resource-group: ${{ github.event.inputs.resource-group }}
            out-file: ${{ github.event.inputs.out-file }}
            sub-name: ${{ github.event.inputs.sub-name }}
        - uses: actions/upload-artifact@v2
          with:
            name: viz
            path: ${{ github.event.inputs.out-file }}
```

## Dependencies

 * [windows-latest](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners#supported-runners-and-hardware-resources)
 * [azure/login](https://github.com/marketplace/actions/azure-login)