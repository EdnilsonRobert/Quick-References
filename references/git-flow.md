# Git Flow | Referência Rápida

## Branches default

``` bash
master
develop
feature    # Commit na branch develop
release    # Commit na branch master e criação de tag
hotfix     # Commit nas branches master e develop
```

## Principais comandos

``` bash
# Para inicializar um repo
git flow init

# Criar uma nova branch feature chamada first-feature
git flow feature start MinhaFeature

# Encerrar a branch realizando o merge na branch develop
git flow feature finish MinhaFeature

# Enviar commit para repo
git flow feature publish MinhaFeature

# Receber uma funcionalidade
git flow feature pull FeatureRecebida
```

## Versões e lançamentos
Branch iniciada a partir de `develop`

``` bash
# Iniciar uma release
git flow release start [versão]
# onde [versão] corresponde ao número de versão

# Publicar uma release
git flow release publish [versão]

# Finalizar uma release
git flow release finish [versão]
```

## Correções [hotfix]

``` bash
# Iniciar uma correção
git flow hotfix start [versão]
# onde [versão] representa a versão defeituosa em produção

# Finalizar uma correção
git flow hotfix finish [versão]
```
