---
title: Entendendo Hooks no React
date: "2020-10-19T00:02:00.121Z"
description: Entenda de uma vez por todas os Hooks no React.
---

Caso você tenha entrado agora no mundo do React, você provavelmente já deve ter ouvido falar sobre "Hooks". Bom, se você nunca ouviu falar, acho que está na hora de conhecer sobre os Hooks.

![React](./img.png)
<hr />

### Os Hooks
Hooks são funções especiais que nos permitem usar funcionalidades que antes eram escritas com classes. Os Hooks nos permitem, também, controlar o estado e o ciclo de vida de componentes funcionais. ["Hooks são funções que permitem a você “ligar-se” aos recursos de state e ciclo de vida do React a partir de componentes funcionais."](https://pt-br.reactjs.org/docs/hooks-overview.html) 

Como eram escritas com classes, não podemos utilizar Hooks dentro de classes. Mas podemos ter um código utilizando Hooks e classe num mesmo projeto. 

De acordo com [a documentação oficial do React](https://pt-br.reactjs.org/docs/hooks-intro.html):
  
  > Eles (Hooks) permitem que você use o state e outros recursos do React sem escrever uma classe.

**States são objetos que contêm dados dentro deles, sendo que esses dados podem ou não ser atualizados.*

Para comerçarmos a utilizar algum Hook, devemos seguir a seguinte estrutura: 

    import React from 'react';

    const App = () => {

      // Abaixo é um Hook.
      const [ativo, setAtivo] = React.useState(false);  // Por convenção, começamos a função atualizadora com "set". Ex: setData, setName, etc.

      // onde: "ativo" é o estado, e o "setAtivo" é a função atualizadora do estado.

      return <h1>Aprendendo Hooks :) </h1>; 
    }

    export default App;
    
 Veja outro exemplo:

    ...

    const App = () => {
      const [data, setData] = React.useState(null);   // Isso é um Hook.

      // "data" é o estado, "setData" é a função atualizadora do estado.
    }

    ...

Os valores presentes dentro dos parênteses são os valores iniciais do estado. Valor pode começar como tipo booleano, como array, objetos, string, etc.

Ou seja, a estrutura padrão de um Hook é assim: 

      const [estado, setEstado] = useState(valorInicialDoEstado); 

Os Hooks foram adicionados na [versão 16.8 do React](https://pt-br.reactjs.org/blog/2019/02/06/react-v16.8.0.html).


### Menos código, mais fácil de entender
Antes da adição de Hooks ao React, quando precisavámos criar um componente, esse componente deveria ser extendido. Então um código que não utilizava Hooks, era escrito da seguinte forma:

      import React from 'react';

      export default class Count extends React.Component {
        constructor(props) {
          super(props);
          this.state = {
            contador: 0, // valor inicial
          };
        }

      render() {
        return (
          <div>
            <h1>Isso é um contador</h1>
            <p>Número atual: {this.state.contador}</p>

            <button
              onClick={() =>
                this.setState((state) => ({ contador: state.contador + 1 }))
              }
            >
              Adicionar mais um
            </button>
          </div>
        );
      };
    };

Agora o mesmo código com Hooks:

    import React from "react";

    const Count = () => {
      const [contador, setContador] = React.useState(0);

      return (
        <div>
          <h1>Isso é um contador</h1>
          <p>Número atual: {contador}</p>

          <button onClick={() => setContador(contador + 1)}>
            Adicionar mais um
          </button>
        </div>
      );
    };

    export default Count;
   
Viu como é mais fácil até para entender? O mesmo código mas com quase dez linhas a menos. Essa é uma das partes mais interessantes dos Hooks. Hoje em dia não precisamos mais de classes, e na <strong>minha opinião</strong> o React fica "complicado" quando utilizamos elas.


### Conhecendo Hooks
Totalizando, o React possui dez Hooks (onze com um Hook customizado). Sendo eles: useState, useEffect, useRef, useContext, useMemo, useCallback, useReducer, [useImperativeHandle](https://pt-br.reactjs.org/docs/hooks-reference.html#useimperativehandle), [useLayoutEffect](https://pt-br.reactjs.org/docs/hooks-reference.html#uselayouteffect), [useDebugValue](https://pt-br.reactjs.org/docs/hooks-reference.html#usedebugvalue) e Hook customizado(nesse post não irei falar sobre useImperativleHandle, useLayoutEffect, useDebugValue).

- ##### useState
É um Hook que te permite adicionar o state do React a um componente de função. Não há limites quanto ao uso do mesmo, você pode utilizá-lo quantas vezes quiser em um código ou aplicação. 

No componente que teremos no trecho de código a seguir iremos utilizar um exemplo real, que é de loading. Enquanto o estado estiver como true, será renderizando um texto com "Carregando...". 

Confira abaixo:

    import React from "react";

    const App = () => {
      const [loading, setLoading] = React.useState(false);

      return (
        <div>
          <h2>Exemplo com useState.</h2>

          {loading && <p>Carregando...</p>}  // Enquanto o estado for igual a true, irá mostra o <p>.

          <button onClick={() => setLoading(!loading)}>   // Com o uso do ponto de exclamação + estado, pegamos o valor anterior comparado ao atual, fazendo um "toggle".
            {loading ? "Cancelar carregamento" : "Carregar"}  // Se estiver carregando, o texto do botão altera.
          </button>
        </div>
      );
    };

      export default App;

Bônus: como pegar um valor de um input escrito pelo usuário e trabalhar com esse valor:

    import React from "react";

    const App = () => {
      const [input, setInput] = React.useState(""); // Estado inicial do input começa como vazio.

      return (
        <div>
          <input
            onChange={({ target }) => setInput(target.value)} // a cada vez que o usuário digitar, pegamos o valor escrito e alteramos o valor do estado com o que ele escreveu.
            value={input} // precisamos colocar que o valor do input é o que o usuário digitar. Então colocamos o estado.
            placeholder="Escreva algo"
          />

          <br />
          
          Você digitou: {input}   // e por final, colocamos o valor do estado aqui.
         </div>
      );
    };

    export default App;




- ##### useEffect
Antes da adição do useEffect, estavámos acostumados a utilizar os seguintes ciclos de vida: componentDidMount, componentDidUpdate e componentWillUnmount. 

Usando o useEffect, diremos ao React que o componente precisa fazer algo quando renderizado. Podemos dizer, também, ao useEffect que ele só irá renderizar um certo trecho de código quando um estado for alterado, por exemplo.  O useEffect é executado a cada renderização.

O useEffect recebe um callback que o mesmo será ativado sempre que um determinado efeito ocorrer. Por exemplo:

      import React from "react";

      const App = () => {
        const [count, setCount] = React.useState(0);

        React.useEffect(() => {
          console.log("página atualizada."); // O console log irá retornar a frase a cada vez que a página for inicializada/atualizada.
        });

        React.useEffect(() => {
          document.title = `Você clicou ${count} vezes.`; // Alteramos o title da página a cada vez que o estado alterar. Exemplo utilizado na documentação oficial.
          console.log("executou");
        });

        return (
          <div>
            <h2>Exemplo com useEffect.</h2>

            <button onClick={() => setCount(count + 1)}>Adicionar</button>
            <p>{`Você clicou ${count} vezes`}</p>
          </div>
        );
      };

      export default App;

Agora imagine que você deseja executar um certo trecho de código apenas uma vez a cada vez que um estado alterar. Isso é possível com o useEffect através de uma "array de dependência". A array de dependência é inserida antes do parentêses final do useEffect e após a virgula (segundo argumento). Assim:

    ...

    React.useEffect(() => {
      console.log("Você clicou");
    },[]);
    // ↳ essa é array de dependência.
      
    // Com essa array vazia, o console.log só será executado uma única vez após a página ser carregada.
    ...

A array de dependência funciona da seguinte forma: o que você colocar dentro dela e o estado daquele item mudar, o código será executado novamente. Caso não mudar, não será executado novamente.

Dica: se você colocar uma array vazia ela não terá dependência alguma. Logo o useEffect será executado apenas uma única vez. 

Caso você esteja se perguntando: podemos sim utilizar o useEffect quantas vezes quisermos, o ideal seria separarmos efeitos diferentes em useEffect's diferentes.

Sempre que você precisar executar um efeito a cada vez que um componente for desmontado (sair de tela/ser removido do DOM), você deve retornar um outro callback retirando o evento, por exemplo: 

      const [scrolled, setScrolled] = React.useState(false);

      React.useEffect(() => {
        const windowScrolled = () => {
          window.pageYOffset > 300 ? setScrolled(true) : setScrolled(false);
        };

        window.addEventListener("scroll", windowScrolled);
        return () => window.removeEventListener("scroll", windowScrolled);  // Retiramos o evento.
      }, []);

PS: Quando você quiser tirar um evento, você deve levar em consideração que você tem que ter definido ele como uma função. Confira abaixo:

      ✔️ Forma correta:
      
      React.useEffect(() => {
        const windowScrolled = () => {
          window.pageYOffset > 300 ? setScrolled(true) : setScrolled(false);
        };

        window.addEventListener("scroll", windowScrolled);
        return () => window.removeEventListener("scroll", windowScrolled); 
      }, []);


      ❌ Forma incorreta:

      React.useEffect(() => {
        window.addEventListener("scroll", () => {
          window.pageYOffset > 300 ? setScrolled(true) : setScrolled(false);
        });
        return () => window.removeEventListener("scroll", () => console.log ("Evento limpo!")); 
      }, []);
Isso acontece pois quando passamos uma função anônima não é possível identificar qual é a função para limpar o evento, e logo não será possível remover/limpar o mesmo.


- ##### useRef
Retorna um objeto com a propriedade ```current```. Você pode usar o useRef quando quiser se referir a um elemento do DOM. Pode ser meio confuso para entender de inicío, mas te darei um exemplo e irei explicar para que você consiga entender da melhor forma. Confira abaixo:

        import React from "react";

        const App = () => {
          const inputFocused = React.useRef();      // Nesse Hook não precisamos utilizar a função atualizadora.
          const [input, setInput] = React.useState("");
          const [message, setMessage] = React.useState(["mensagem 1, mensagem 2"]);

          function handleMessage() {
            setMessage([...message, input]);  // pegamos o valor inicial do "message". Adicionamos também o valor do input escrito pelo usuário
            inputFocused.current.focus();   // quando o usuário enviar a mensagem, o input será focado utilizando o ref.current
            setInput('');  // após o envio da mensagem, limpamos o input.
          }

          return (
            <div>
              <input
                onChange={({ target }) => setInput(target.value)}
                value={input}
                placeholder="Escreva uma mensagem"
                ref={inputFocused}    // devemos utilizar o "ref" e atribuir a variavel que criamos lá em cima.
              />
              <ul>
                {message.map(message => (
                  <li>{message}</li>
                ))};
              </ul>
              <button onClick={handleMessage}>Enviar mensagem</button>
            </div>
          );
        };

        export default App;


- ##### useMemo
O useMemo retorna um valor [memoizado](https://en.wikipedia.org/wiki/Memoization). O useMemo é utilizado quando você quer evitar a recriação de algo quando um componente for atualizado. Assim como o useEffect, ele recebe um callback e array de dependências.

        import React from "react";

        const App = () => {
          const [contador, setContador] = React.useState(0);

          React.useMemo(() => {
            console.log("Memo executado.");
          }, []);

          return (
            <div>
              <div>{contador}</div>
              <button onClick={() => setContador(contador + 1)}>Contar mais um</button>
            </div>
          );
        };

        export default App;


- ##### useCallback
O useCallback retorna um callback [memoizado](https://en.wikipedia.org/wiki/Memoization). Esse Hook nos permite memorizar funções e prevenir que as mesmas sejam criadas a cada novo render de um componente. Assim como o useEffect e o useMemo, ele recebe um callback e array de dependências. 

Um exemplo bem simples é com o uso de ```handleClick``` que é um callback.

    import React from "react";

    const App = () => {
      const [contador, setContador] = React.useState(0);

      const handleCkick = React.useCallback(() => {
        setContador((contador) => contador + 1);
        console.log("Botão clicado.");
      }, []);

      return (
        <div>
          <div>{contador}</div>
          <button onClick={handleCkick}>Contar mais um</button>
        </div>
      );
    };

    export default App;

- ##### useContext
O useContext é utilizado quando queremos passar um estado/dado para algum componente sem utilizar as propriedades. Um exemplo bem comum e bastante utilizado é quando o usuário está logado.

Parar criar um contexto é recomendado criar um componente específico para tal.

```Arquivo UserContext.js```:

      import React from 'react';

      const UserContext = React.createContext();
      
      export default UserContext;

Devemos colocar o contexto na parte mais global de sua aplicação. Geralmente no App.js.

```Arquivo App.js```:

    import React from 'react';
    import UserContext from './UserContext';

    const App = () => {
      const dados = React.useContext(UserContext);

      return (
        <UserContext.Provider value={{nome: "Caio"}}>  // Devemos colocar o .Provider pois é um método. Devemos, também, colocar o value.
          <div></div>   // agora essa div tem acesso ao contexto.
        </UserContext.Provider>
      );
    };
     
    export default Pessoa;

OBS: Dentro de ```value``` podemos passar qualquer tipo de dado, seja string, estado, etc.

Agora precisamos usar o contexto criado.

```Arquivo Pessoa.js```:

    import React from 'react';
    import UserContext from './UserContext';

    const Pessoa = () => {
      const dados = React.useContext(UserContext);

      return (
        <p>{dados.nome}</p>;  // Retorna "Caio"
      );
    };
     
    export default Pessoa;


- ##### useReducer
Caso você já esteja familiarizado com o [Redux](https://redux.js.org) o useReducer fica fácil. Mas caso você não esteja, irei te ensinar.
 
Iremos utilizar o useReducer quando quisermos lidar com estados que possuem diversas funções que modificam os mesmos.


Esse Hook recebe dois argumentos:
- Função redutora;
- Estado inicial.


A função ```reducer```, abaixo, também recebe dois argumentos:
- Estado atual;
- Ação.


O useReducer segue a seguinte estrutura:

    import React from "react";

      function reducer(state, action) {   // onde: state é o estado e action é a ação.
        switch (action) {
          case 'aumentar':   // caso clicar no botão aumentar, ele irá retornar o estado atual + 1;
            return state + 1;
          case 'diminuir':   // caso clicar no botão aumentar, ele irá retornar o estado atual - 1;
            return state -1;  
          default:
            throw new Error();    // irá retornar erro caso o nome da action for incorreto. Por exemplo: 'almentar'.
        }

        // pode-se usar if no lugar de switch.
      }
        
      const App = () => {
        const [contador, dispatch] = React.useReducer(reducer, 0);

        // onde: reducer é a função redutora e 0 é o estado inicial.

        return (
          <div>
            <p>{contador}</p>
            <button onClick={() => dispatch('aumentar')}>Aumentar</button>
            <button onClick={() => dispatch('diminuir')}>Diminuir</button>
          </div>
        );
      };

      // Dispatch é a função que irá enviar as ações para o reducer. As ações podem ser diversas. Por exemplo: ação de aumentar, ação de diminuir.
      
      export default App;

A função ```reducer``` é ativada apenas quando o ```dispatch``` é ativado.

- ##### Custom Hooks
Também é possível criar seu próprio Hook e utilizar durante toda sua aplicação. Todo custom Hook deve começar com "use". Por exemplo: ```useNomeDoHook```.

Um custom Hook pode retornar o que você bem quiser, como um objeto, array, etc. 

    ...

    const useLocalStorage = (key, valor) => {
      const [state, setState] = React.useState(() => {
        const item = window.localStorage.getItem(key);
        return item ? item : valor;
      });

      React.useEffect(() => {
        window.localStorage.setItem(key, state);
      }, [key, state]);

      return [state, setState];
    }

    ...

Geralmente é criada uma pasta específica apenas para custom Hooks.

### Regras
  Devemos seguir algumas regras quanto ao uso dos Hooks.
- Não utilize Hook algum dentro de condicionais, funções ou em laços de repetição;

        ❌ Incorreto:

        const estado = false;
        if(!estado) {
          React.useEffect(() => {
            console.log('Essa é uma forma incorreta!!');
          }, []);
        }

        ❌ Incorreto:
        
        function alerta() {
          React.useEffect(() => {
            alert('Essa é uma forma incorreta!!!');
          }, []);
        }

        ✔️ Correto:

        React.useEffect(() => {
          console.log('Essa é uma forma correta!');
        }, []);
        

        ❌ Incorreto:

        for(let i = 0; i <= 10, i++) {
          React.useEffect(() => {
            console.log('Mais uma forma incorreta.')
          }, [])
        }
- Utilize Hooks apenas em components e em Hooks Customizados.  

### Conclusão
Como pudemos ver, os Hooks são uma maravilha e com certeza nos ajudam bastante. Pudemos ver, também, que quando escrevemos utilizando os Hooks o código mais fácil de entender e com menos linhas de códigos. De inicío Hooks são bem complicados de se entender, mas com a prática você consegue entender todos.

Diante disso, podemos sim utilizar Hooks e classes num mesmo projeto, como mencionado anteriormente. Entretanto, em <strong>minha opinião</strong> o conceito de classes no React morre com a chegada dos Hooks. 

Durante muito tempo muitas aplicações React foram desenvolvidadas com classes, até mesmo algumas libs continuam usando classes. 

Sobretudo, você ainda pode sim utilizar classes sem problemas.

Esse post foi escrito com muito cuidado e carinho. Eu já possuo experiência com os Hooks, mas dei uma revisada através de e-books, vídeo-aulas, etc. para trazer um conteúdo bem completo e detalhado. Espero que você tenha gostado. 

Caso você deseja aprofundar seus conhecimentos com React, recomendo os seguintes canais:

- [Rocketseat](https://www.youtube.com/channel/UCSfwM5u0Kce6Cce8_S72olg);
- [Bonieky Lacerda](https://www.youtube.com/c/BoniekyLacerdaLeal/videos);
- [Origamid](https://www.youtube.com/user/origamidlabs);

e até mesmo a própria [documentação do React](https://pt-br.reactjs.org) que foi bastante consultada para escrever esse post.

No mais, isso é tudo. Obrigado e até à próxima!


*Referências: https://br.bitdegree.org/tutoriais/react-js/#heading-2, https://pt-br.reactjs.org/docs/hooks-intro.html, https://pt-br.reactjs.org/docs/hooks-rules.html*
