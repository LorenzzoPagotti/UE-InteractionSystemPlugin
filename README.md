# UE-InteractionSystemPlugin

# Modular Interaction Component for Unreal Engine

A C++ Actor Component for Unreal Engine that provides a modular, performant, and flexible interaction system. This component allows a character to interact with any actor in the world that implements a specific interface, featuring an optional and optimized visual feedback system.

---

## Features

* **100% Modular:** Add the `UInteractionComponent` to any actor (character, NPC, etc.) to give it the ability to interact with the world.
* **Highly Performant:** Object detection for visual feedback runs on a **Timer** with a customizable frequency, instead of the frame's `Tick`, ensuring minimal performance impact.
* **Decoupled Logic:** The component uses **Delegates** (`OnInteractionActorChanged`) to communicate with the UI in a decoupled manner.
* **Robust and Safe:** The core interaction logic (`Interaction()`) is self-sufficient and works perfectly, even if the visual feedback system is disabled.
* **Easy to Customize:** Properties like interaction distance (`TraceReach`), check frequency (`InteractionCheckRate`), and UI activation (`bShowInteractionUI`) are easily configurable via the Details Panel in the editor.

---

## How to Use

To integrate this system into your project, follow the 4 steps below:

### 1. Add the Component to the Character

* Open your character's Blueprint.
* Click `+ Add` and add the `InteractionComponent`.
* In the character's `Event Graph`, create the input logic (e.g., on pressing the **E** key), get a reference to the `InteractionComponent`, and call the `Interaction` function.
* 
### 2. Prepare the Interactable Actor

Any actor you want to be "interactable" (a door, a button, an item) must implement the "InteractionInterface" OR be a child of "BaseInteractionActor" class.

* Open your actor's Blueprint (e.g., `BP_Door`).
* Go to `Class Settings` and add the `Interaction_Interface` interface to the `Implemented Interfaces` list.
* Implement the `Interact` event in your Event Graph. The logic inside this event is what will happen when the player interacts with the object.

### 3. Configure the UI (Optional)

If you've enabled the `bShowInteractionUI` option in the component, your UI can react to focus changes.
* Create a Widget Blueprint for your interaction prompt (e.g., `WBP_InteractionWidget`).
* In the widget's `Event Graph`, on the `Event Construct` event, get a reference to the player's `InteractionComponent`.
* Drag the pin from the component and use the **`Bind Event to OnInteractionActorChanged`** node.
* The triggered event will give you the new focused actor (`NewFocusedActor`). Use an `IsValid` node to check if the actor is valid. If it is, show the widget; if not, hide it.

---

## Customization in the Editor

You can customize the component's behavior directly in your character's Details Panel.

| Property | Description |

| **Trace Reach** | The maximum distance, in units, that the character can reach to interact. |
| **Interaction Check Rate** | The frequency (in seconds) at which the system checks what the player is aiming at. Lower values are more responsive but consume more performance. |
| **Show Interaction UI** | Enables or disables the check and event for visual UI feedback. The core interaction still works even if disabled. |

<details>
<summary><strong>Ver em Português 🇧🇷</strong></summary>

# Componente de Interação Modular para Unreal Engine

Um Componente de Ator (Actor Component) em C++ para a Unreal Engine que fornece um sistema de interação modular, performático e flexível. Este componente permite que um personagem interaja com qualquer ator no mundo que implemente uma interface específica, apresentando um sistema de feedback visual opcional e otimizado.

---

## Funcionalidades

* **100% Modular:** Adicione o `UInteractionComponent` a qualquer ator (personagem, NPC, etc.) para dar a ele a capacidade de interagir com o mundo.
* **Altamente Performático:** A detecção de objetos para o feedback visual roda em um **Timer** com frequência customizável, em vez de usar o `Tick` do frame, garantindo um impacto mínimo na performance.
* **Lógica Desacoplada:** O componente utiliza **Delegates** (`OnInteractionActorChanged`) para se comunicar com a UI de forma desacoplada.
* **Robusto e Seguro:** A lógica principal de interação (`Interaction()`) é autossuficiente e funciona perfeitamente, mesmo que o sistema de feedback visual esteja desativado.
* **Fácil de Customizar:** Propriedades como distância da interação (`TraceReach`), frequência da verificação (`InteractionCheckRate`) e ativação da UI (`bShowInteractionUI`) são facilmente configuráveis através do Details Panel no editor.

---

## Como Usar

Para integrar este sistema ao seu projeto, siga os 3 passos abaixo:

### 1. Adicione o Componente ao Personagem

* Abra o Blueprint do seu personagem.
* Clique em `+ Add` e adicione o `InteractionComponent`.
* No `Event Graph` do personagem, crie a lógica de input (ex: ao pressionar a tecla **E**), pegue uma referência ao `InteractionComponent` e chame a função `Interaction`.

### 2. Prepare o Ator Interagível

Qualquer ator que você queira que seja "interagível" (uma porta, um botão, um item) deve implementar a interface `InteractionInterface` OU ser uma classe child de `BaseInteractionActor`.

* Abra o Blueprint do seu ator (ex: `BP_Door`).
* Vá em `Class Settings` e adicione a interface `Interaction_Interface` à lista de `Implemented Interfaces`.
* Implemente o evento `Interact` no seu Event Graph. A lógica dentro deste evento é o que acontecerá quando o jogador interagir com o objeto.

### 3. Configure a UI (Opcional)

Se você ativou a opção `bShowInteractionUI` no componente, sua UI pode reagir às mudanças de foco.
* Crie um Widget Blueprint para seu aviso de interação (ex: `WBP_InteractionWidget`).
* No `Event Graph` do widget, no evento `Event Construct`, obtenha uma referência ao `InteractionComponent` do jogador.
* Arraste o pino do componente e use o nó **`Bind Event to OnInteractionActorChanged`**.
* O evento disparado lhe dará o novo ator em foco (`NewFocusedActor`). Use um nó `IsValid` para verificar se o ator é válido. Se for, mostre o widget; se não, esconda-o.

---

## Customização no Editor

Você pode customizar o comportamento do componente diretamente no Details Panel do seu personagem.

| Propriedade | Descrição |
| :--- | :--- |
| **Trace Reach** | A distância máxima, em unidades, que o personagem consegue alcançar para interagir. |
| **Interaction Check Rate** | A frequência (em segundos) com que o sistema verifica o que está na mira do jogador. Valores menores são mais responsivos, mas consomem mais performance. |
| **Show Interaction UI** | Ativa ou desativa a verificação e o evento para o feedback visual da UI. A interação principal continua funcionando mesmo se desativado. |

</details>
| **Show Interaction UI** | Enables or disables the check and event for visual UI feedback. The core interaction still works even if disabled. |

