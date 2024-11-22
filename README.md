# Experiências Imersivas: Realidade Aumentada e Tour 360°

Este projeto foi desenvolvido para explorar experiências imersivas utilizando as tecnologias **A-Frame** e **AR.js**. Ele inclui duas soluções principais:

1. **Realidade Aumentada (AR)** com o uso de um marcador Hiro.
2. **Tour 360°** navegável por ambientes virtuais. 

Uma página inicial serve como ponto de partida para escolher entre essas duas experiências.

---

## Tecnologias Utilizadas

- **A-Frame**: Framework para criação de experiências de realidade virtual baseadas em HTML e JavaScript.
- **AR.js**: Biblioteca para realidade aumentada, integrável com A-Frame, especialmente para cenários baseados em marcadores e localização.

---

## Estrutura do Projeto

### 1. Página Inicial `index.html`

Essa página inicial permite ao usuário escolher entre a experiência de Realidade Aumentada ou o Tour 360°. Ela contém dois botões estilizados com CSS que direcionam para as páginas correspondentes.

```html
<div class="container">
    <h1>Escolha sua Experiência</h1>
    <div class="button-container">
        <a href="tour360.html" class="btn">Tour 360°</a>
        <a href="realidadeAumentada.html" class="btn">Realidade Aumentada</a>
    </div>
</div>
```

- **Função**: Este trecho cria uma interface simples para seleção da experiência desejada.
- **CSS**: Adiciona um design moderno com gradientes de fundo e botões estilizados para melhorar a experiência do usuário.

---

### 2. Realidade Aumentada (AR): `realidadeAumentada.html`

Nesta página, a experiência de AR utiliza um marcador Hiro para exibir um vídeo em um espaço tridimensional.

```html
<a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
    <a-assets>
        <video id="video" src="https://cdn.glitch.global/<project-id>/test.mp4"></video>
    </a-assets>
    <a-marker preset="hiro" controlador>
        <a-video width="1" height="1" rotation="-90 0 0" position="0 0 0" src="#video"></a-video>
    </a-marker>
    <a-entity camera></a-entity>
</a-scene>
```

- `<a-scene>`: Configura a cena para AR, desativando a interface de realidade virtual (vr-mode-ui) e habilitando o uso de marcadores (arjs).
- `<a-marker>`: Define o marcador Hiro como referência visual para renderizar o vídeo.
- `<a-assets>`: Gerencia os recursos, como vídeos ou modelos, para serem usados na cena.
- `<a-video>`: Renderiza o vídeo dentro do marcador Hiro, com dimensões, rotação e posição ajustadas.
- **Componente Personalizado**: O código JavaScript pausa e reproduz o vídeo com base na visibilidade do marcador:

```js
AFRAME.registerComponent('controlador', {
    init: function () {
        this.toggle = false;
        this.vid = document.querySelector("#video");
        this.vid.pause();
    },
    tick: function () {
        if (this.el.object3D.visible == true) {
            if (!this.toggle) {
                this.toggle = true;
                this.vid.play();
            } else {
                this.toggle = false;
                this.vid.pause();
            }
        }
    }
});
```
---

### 3. Tour 360°: `tour360.html` e relacionados

O Tour 360° apresenta um ambiente imersivo com imagens panorâmicas, permitindo navegação entre diferentes "salas" por meio de elementos interativos.

```html
<a-scene>
    <a-assets>
        <img id="img" src="https://cdn.glitch.global/<project-id>/hall.jpeg" />
    </a-assets>
    <a-sky id="img-360" src="#img"></a-sky>
    <a-sphere id="vai_para_cima" position="-8 10 -26" radius="0.5" color="#ed1212"></a-sphere>
</a-scene>
```

- `<a-sky>`: Define o ambiente 360°, utilizando uma imagem panorâmica como textura.
- `<a-sphere>`: Cria um elemento interativo que atua como "porta" para a próxima sala.
- **Transição de Cena:** Um evento JavaScript redireciona o usuário para outra página ao interagir com o objeto:

```js
document.querySelector("#vai_para_cima")
    .addEventListener("mouseenter", e => {
        location.href = "index2.html";
    });
```

---

## Conclusão

Este projeto demonstra como as ferramentas A-Frame e AR.js podem ser combinadas para criar experiências imersivas, tanto em Realidade Aumentada quanto em Realidade Virtual.

- A solução de AR com marcadores Hiro oferece uma interação simples e envolvente.
- O tour 360° destaca o potencial de ambientes virtuais exploráveis, que podem ser adaptados para jogos, educação, ou apresentações empresariais.

A modularidade e simplicidade do código permitem expandir essas aplicações para novos cenários e experiências, consolidando a base para futuros desenvolvimentos na área de entretenimento imersivo.