# Pour forcer une surcharge sur Linux

## Etape 1 : Installer le paquet stress
```apt-get update && apt-get install -y stress```

## Lancer un stress
```stress --cpu X --timeout Y```
=> Permet de lancer un nombre de worker (X) et pendant un certain temps (Y) en secondes.

```stress --vm 1 --timeout Ys```
=> Permet de chargeer / décharger la mémoire pendant X temps 

==> Idéal pour simuler lors de la supervision
