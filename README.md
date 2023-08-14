import 'package:flutter/material.dart';


void main() {
  runApp(
    const MaterialApp(
      title: "Cadastro",
      home: Cadastro(),
    ),
  );
}


class Cadastro extends StatefulWidget {
  const Cadastro({super.key});

  @override
  State<Cadastro> createState() => _CadastroState();
}

class _CadastroState extends State<Cadastro> {
  final TextEditingController _usuarioControle =
      TextEditingController(); //o " _ " significa que é privado da classe
  final TextEditingController _senhaControle = TextEditingController();

  String _bemvindo = ""; // Iniciar limpo o campo do texto

  void _mostraBemVindo() {
    setState(() {
      //os valores vão mudar
      //existe forma de fazer melhor, mas por enquanto vamos ficar com essa
      //Controle de usuario e senha

      if (_usuarioControle.text.isNotEmpty && _senhaControle.text.isNotEmpty) {
        _bemvindo = "Olá, ${_usuarioControle.text}!";
      }
    });
  }

  void _cancelar() { //Botão cancelar
    //quando clicar em cancelar vai limpar os campos do nome, senha e o texto
    setState(() {
      _usuarioControle.clear();
      _senhaControle.clear();
      _bemvindo = "";
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold( //Um widget responsável por criar um layout “padrão” para o app, contendo uma appBar e o conteúdo da tela.
    //appBar, backgroundColor e body

      appBar: AppBar(
        title: const Text(
            "Cadastro"), //const para aquilo que sabemos que não vai ser alterado, não vai mudar
        backgroundColor: Color.fromARGB(255, 147, 233, 207),
      ),

      backgroundColor: Color.fromARGB(255, 123, 206, 206),

      body: Container( //Usamos um Conteiner quando desejamos adicionar preenchimento (padding),
      // margens, bordas ou cor de fundo para nomear alguns de seus recursos. 

        alignment: Alignment.topCenter,
        child: ListView( // Uma lista rolável de widgets organizados linearmente.

          children: <Widget>[ //Lista de Widgets
            Padding(
              padding: const EdgeInsets.all(10.0),
              child: Image.asset( //Imagem Logo, no topo
                'assets/kauane_.png',
                height: 130.0,
                //color: Colors.white, //modificar a cor da imagem
              ),
            ),

            //Cadastro // formulário
            Padding(
              padding:
                  const EdgeInsets.only(left: 20.0, right: 20.0, top: 40.0),

              child: Container(
                width: double.infinity, //define uma largura mais flexível

                color: Color.fromARGB(255, 223, 156, 236),
                child: Column(
                  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                  //alinhamento do eixo principal *spaceEvenly tudo ficara separado igualmente

                  children: <Widget>[
                    Padding(  //NOME
                      padding: const EdgeInsets.all(8.0),
                      child: TextField( //permitem que os usuários digitem texto
                        controller: _usuarioControle, // Controller servem para você, através de eventos, 
                        //conseguir controlar algum recurso, como um campo de texto ou um formulário.

                        decoration: InputDecoration(
                          hintText:
                              'Nome', //Frase que fica no campo para informar o usuário o que deve por no campo
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(20.0),
                          ),
                          icon: const Icon(Icons.person_2_outlined), // Icone na lateral esquerda do TextField
                        ),
                      ),
                    ),


                    Padding( //SENHA
                      padding: const EdgeInsets.all(8.0),
                      child: TextField( //caixa de texto
                        controller: _senhaControle,
                        decoration: InputDecoration(
                          hintText:
                              'Senha', //Frase que fica no campo para informar o usuário o que deve por no campo
                          border: OutlineInputBorder(
                            borderRadius: BorderRadius.circular(20.0),
                          ),
                          icon: const Icon(Icons.key),
                        ),
                        obscureText: true, //Esconder o texto quando digitar a senha
                      ),
                    ),


                    Center(
                      child: Row( //para os botões ficarem na horizontal // um do lado do outro
                        mainAxisAlignment: MainAxisAlignment.spaceEvenly, //espaço entre os botões mesmo se mudar de direção a tela

                        children: <Widget>[ 
                          //Enter
                          ElevatedButton( //Um "botão elevado" do Material Design.
                          
                            style: ElevatedButton.styleFrom(
                              backgroundColor: Color.fromARGB(255, 211, 130, 208), //cor do botão
                              foregroundColor: Color.fromARGB(255, 87, 192, 192), //cor da letra do botão
                            ),
                            onPressed: _mostraBemVindo,
                            child: const Text(
                              "Entrar",
                            //  style: TextStyle(fontSize: 20), //tamanho da letra
                            ),
                          ),

                          //Cancel
                          ElevatedButton(
                            style: ElevatedButton.styleFrom(
                              backgroundColor: Color.fromARGB(255, 221, 144, 204), //cor do botão
                              foregroundColor: Color.fromARGB(255, 62, 121, 119), //cor da letra do botão
                            ),
                            onPressed: _cancelar,
                            child: const Text(
                              "Cancelar",
                              //  style: TextStyle(fontSize: 20), //tamanho da letra
                            ),
                          ),
                        ],
                      ),
                    ),
                  ],
                ),
              ),
            ),

            //Text abaixo dos botões
            Padding(
              padding: const EdgeInsets.all(40.0),
              child: Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  Text(
                    _bemvindo, 
                    style: const TextStyle(
                      color: Color.fromARGB(255, 201, 154, 216),
                      fontSize: 30.0,
                      fontWeight: FontWeight.w500,
                    ),
                  ),
                ],
              ),
            )
          ],
        ),
      ),
    );
  }
}

