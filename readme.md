# PASSO-A-PASSO E PACOTES INSTALADOS

Inicia o GIT no projeto
```
git init
```

Criar o package.json
```
yarn init
```

Instalar pacotes do commitlint
```
yarn add @commitlint/config-conventional @commitlint/cli -D
```

Rodar a linha a abaixo para criar o arquivo commitlint.config.js. Mas o melhor seria criar o arquivo do zero e inserir o conteúdo do echo"", pois tive problemas de encoding do arquivo js.
```
echo "module.exports = {extends: ['@commitlint/config-conventional']}" > commitlint.config.js
```

Instalar o pacote do husky
```
yarn add husky -D
```

Após a linha de "license" no package.json colocar uma virgula e na linha abaixo inserir o trecho abaixo
```json
"husky": {
  "hooks": {
    "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
  }  
}
```

Com commitlint as mensagens de commit devem seguir um padrão. Exemplo:
```
git commit -m "feat(financeiro): Implementação do combos de formas de pagamento
```

Sempre seguindo o padrão disponível em [https://commitlint.js.org/#/concepts-commit-conventions](https://commitlint.js.org/#/concepts-commit-conventions)
```
type(scope?): subject
body?
footer?
```
Instalar o pacote do commitizen
```
yarn add commitizen -g
```

Como estou usando Yarn executo a linha abaixo. Para NPM consulte a documentação.
```
commitizen init cz-conventional-changelog --yarn --dev --exact
```

Incluir no package.json o trecho abaixo
```json
"scripts":{
  "commit": "git-cz"
},
```

Agora com o commitizen instalado tudo fica mais simples e automatizado. Para fazer um commit agora se usa:
```
yarn commit
```

Para tentar melhorar, dentro de package.json, husky > hooks, abaixo de commit-msg, se coloca este trecho abaixo.
```json
"prepare-commit-msg": "exec < /dev/tty && git cz --hook || true",
```

Com o trecho acima a documentação diz que apenas se usa
```
git commit
```

Após isso pode até excluir o trecho do package.json. Uma dica minha, eu tive problemas em usar apenas ```git commit```, então sugiro usar apenas ```yarn commit```, e desconsiderar o trecho do ```prepare-commit-msg```. Talvez seja alguma limitação do Windows, não sei bem. Mas cada teste no seu ambiente e veja o resultado.
```json
"scripts":{
  "commit": "git-cz"
},
```

# Fontes

- [https://github.com/conventional-changelog/commitlint](https://github.com/conventional-changelog/commitlint)
- [https://commitlint.js.org/#/](https://commitlint.js.org/#/)
- [https://github.com/commitizen/cz-cli](https://github.com/commitizen/cz-cli)
- [https://yarnpkg.com/en/docs/cli/run](https://yarnpkg.com/en/docs/cli/run)
- [https://www.youtube.com/watch?time_continue=34&v=erInHkjxkL8&feature=emb_logo](https://www.youtube.com/watch?time_continue=34&v=erInHkjxkL8&feature=emb_logo)

[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)