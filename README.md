# spk-assist -  versão 1.0
Pequeno (menos de 20 linhas) assistente de fala em shell script para pessoas com limitações motoras impossibilitadas de falar.

Vídeo de demonstração [no Youtube](https://youtu.be/dhQKBfmiKYs).

## Justificativa

Este script foi inspirado no projeto [PRIsh](https://github.com/projeto-pri/prish), parte do **Projeto PRI**, que é um utilitário em linha de comando para auxiliar pessoas que estão passando por alguma condição médica que limite seus movimentos e as impeça de falar, como vítimas de um AVC, por exemplo. Contudo, a nossa proposta difere em alguns pontos:

1. Nosso script foi pensado para uma variedade maior de dispositivos de entrada, incluindo a possibilidade de interação via mouse e os controladores de jogos universais mais simples.
2. Nós pretendemos implementar áudios previamente gravados, como no projeto original, mas estamos priorizando a sintetização de voz como alternativa padrão. Deste modo, qualquer alteração na lista de frases (arquivo `spk-assist-sentences`) estará automaticamente disponível, sem a necessidade de esperar a gravação de novos áudios.
3. Em vez de pensarmos em frases completas, nossa proposta é trabalhar com "prefixos" e "complementos", de modo que, em apenas duas etapas, o usuário seja capaz de gerar combinações complexas e mais diversificadas.

No mais, o `spk-assist` é um software 100% livre, com foco em usabilidade, portabilidade dentro do universo Linux, altamente personalizável, e extremamente simples.

> **Observação:** o `spk-assist` não foi criado no intuito de ser melhor do que o **Projeto PRI** nem pretende desmerecer o trabalho dos seus desenvolvedores. Muito pelo contrário! A nossa ideia (e já estamos fazendo isso) é estudar o código original e contribuir (com código) para que ele ofereça ainda mais alternativas de uso. O nosso objetivo aqui é apenas apresentar uma outra visão sobre como atingir o mesmo propósito e descobrir como aplicar as soluções que encontrarmos ao projeto original.

## Dependências

* Algorítimo de sintetização de voz MBROLA, especialmente os pacotes `mbrola-br1` (voz masculina) e `mbrola-br4` (voz feminina);
* Sintetizador de voz `espeak`
* Buscador interativo para a linha de comando `fzf`

É bem provável que essas dependências sejam encontradas em qualquer distribuição. No **Debian** e derivados, elas são instaladas com o comando abaixo:

```
sudo apt install fzf espeak mbrola-br*
```

## Instalação

Basta clonar este repositório, entrar na pasta criada pelo terminal e executar o comando `./spk-assist`.

```
git clone https://github.com/debxp/spk-assist.git

cd spk-assist
./spk-assist
```

**Alternativamente**, você pode baixar a versão *zip*, descompactar o arquivo, entrar na pasta onde se encontra o script e executá-lo.

> **Atenção, importante!**  
> 
> Os arquivos `spk-assist` e `spk-assist-sentences` devem estar obrigatoriamente na mesma pasta!

## Configuração

No arquivo `spk-assist-sentences`, existem dois grupos de frases: as **frases simples** (numeradas) e as **frases compostas**. Nos dois casos, as frases são compostas de um prefixo e uma lista de complementos, no formato abaixo:

```
frase["prefixo"]="complemento 1|complemento 2|...complemento n"
```

O prefixo será exibido na primeira listagem que o script apresenta. Ao selecioná-lo, será exibida uma segunda listagem com as falas correspondentes aos complementos configurados.

> **Atenção, importante!**
> 
> As frases de complemento devem ser separadas por uma barra vertical (`|`) e não pode haver espaços entre elas.

Exemplo de uma **frase composta**:

```
frase["pegue"]="um travesseiro|meus remédios|os meus óculos"
```

Na configuração, a diferença das frases simples é que o prefixo deve ser antecedido de um número de **1** a **9**. Por exemplo:

```
frase["1-rápidas"]="Fogo! Chame os bombeiros!|Socorro! Chame uma ambulância!|Está doendo!"
frase["2-perguntas"]="que horas são?|tudo bem?|quando você volta?"
```

Essa padronização foi feita para que as frases mais diretas ou urgentes sejam sempre as primeiras opções nas listagens. Além disso, **os prefixos numerados não serão vocalizados**, apenas seus complementos.

## O futuro

No futuro (próximo), nós pretendemos...

* Implementar a opção de executar áudios gravados (o problema é gravar)
* Modificar a forma como as frases são configuradas no arquivo `spk-assist-sentences`
* Formatar a exibição do fzf
* Implementar o teste de dependências