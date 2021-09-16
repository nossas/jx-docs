---
title: Acelerar
linktitle: Acelerar
description: Como acelerar a entrega de valor ao cliente
type: docs
weight: 20
---

Jenkins X é uma implementação de CI/CD reimaginada para a núvem que é fortemente influenciada pelos relatórios do State of DevOps e, mais recentemente, pelo livro [Accelerate] (https://www.amazon.co.uk/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339) de [Nicole Forsgren](https://twitter.com/nicolefv), [Jez Humble](https://twitter.com/jezhumble) e [Gene Kim](https://twitter.com/RealGeneKim?).

<img src="/images/accelerate.jpg" class="img-thumbnail" width="500" height="750">

Anos de coleta de dados por equipes e organizações do mundo real que foram analisados por líderes inovadores e cientistas de dados do mundo DevOps. O livro Accelerate recomenda uma série de recursos que o Jenkins X está implementando para que os usuários obtenham os benefícios cientificamente comprovados, prontos para o uso. Começamos a documentar os recursos que estão disponíveis hoje e vamos continuar conforme eles se expandam.

<img src="/images/capabilities.png" class="img-thumbnail" width="400" height="750">

# Use o controle de versão para todos os artefatos

O pessoal da Weaveworks cunhou o termo GitOps que amamos. Qualquer mudança em um ambiente, seja um novo aplicativo, atualização de versão, alteração de limite de recursos ou configuração de um simples aplicativo, deve ser gerada como uma solicitação pull para o Git, ter verificações executadas nele como uma forma de CI para ambientes e aprovado por uma equipe que tem controle sobre o que acontece no ambiente relacionado. Agora permitimos que a liderança tenha total rastreabilidade para qualquer mudança em um ambiente.

# Automatize seu processo de deploy

## Ambientes

O Jenkins X irá, por meio do Git, criar ambientes automaticamente durante a instalação e tornar fácil a adição de novas utilizando `jx create environment`. Além disso, quando criamos novas aplicações por um quickstart (`jx create quickstart`), SpringBoot baseado em Java (`jx create spring`) ou importando aplicações existentes (`jx import`), Jenkins X irá automaticamente adicionar pipelines de CI/CD e as configurações dos trabalhos, repositórios git e webhooks para habilitar um processo de deploy automatizado.

Pronto para utilizar, Jenkins X cria ambientes permanentes de Staging e Produção (customizáveis) assim como ambientes temporários para aplicações de visualização de Pull Requests.