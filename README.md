flutter create cp5_forms_rm94654

import 'package:flutter/material.dart';
import 'package:nome_do_projeto/success_screen.dart';

class FormScreen extends StatefulWidget {
  @override
  _FormScreenState createState() => _FormScreenState();
}

class _FormScreenState extends State<FormScreen> {
  final _formKey = GlobalKey<FormState>();
  String _name = '';
  String _lastName = '';
  String _email = '';
  String _password = '';

  void _saveForm() async {
    if (_formKey.currentState!.validate()) {
      _formKey.currentState!.save();

      await Future.delayed(Duration(seconds: 1));

      showDialog(
        context: context,
        builder: (ctx) => AlertDialog(
          title: Text('Sucesso', style: TextStyle(color: Colors.teal)),
          content: Text('Os dados foram salvos com sucesso!'),
          actions: [
            TextButton(
              onPressed: () {
                Navigator.of(ctx).pop();
                Navigator.of(context).pushReplacement(
                  MaterialPageRoute(
                    builder: (context) => SuccessScreen(
                      name: _name,
                      lastName: _lastName,
                      email: _email,
                      password: _password,
                    ),
                  ),
                );
              },
              child: Text('OK', style: TextStyle(color: Colors.teal)),
            ),
          ],
        ),
      );
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Formulário', style: TextStyle(color: Colors.white)),
        backgroundColor: Colors.teal,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            children: [
              TextFormField(
                decoration: InputDecoration(
                  labelText: 'Nome',
                  border: OutlineInputBorder(),
                  prefixIcon: Icon(Icons.person, color: Colors.teal),
                ),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Por favor, insira o nome';
                  }
                  return null;
                },
                onSaved: (value) {
                  _name = value!;
                },
              ),
              SizedBox(height: 16),
              TextFormField(
                decoration: InputDecoration(
                  labelText: 'Sobrenome',
                  border: OutlineInputBorder(),
                  prefixIcon: Icon(Icons.person_outline, color: Colors.teal),
                ),
                onSaved: (value) {
                  _lastName = value!;
                },
              ),
              SizedBox(height: 16),
              TextFormField(
                decoration: InputDecoration(
                  labelText: 'Email',
                  border: OutlineInputBorder(),
                  prefixIcon: Icon(Icons.email, color: Colors.teal),
                ),
                keyboardType: TextInputType.emailAddress,
                validator: (value) {
                  if (value == null || !value.contains('@')) {
                    return 'Por favor, insira um email válido';
                  }
                  return null;
                },
                onSaved: (value) {
                  _email = value!;
                },
              ),
              SizedBox(height: 16),
              TextFormField(
                decoration: InputDecoration(
                  labelText: 'Senha',
                  border: OutlineInputBorder(),
                  prefixIcon: Icon(Icons.lock, color: Colors.teal),
                ),
                obscureText: true,
                validator: (value) {
                  if (value == null || value.length < 6) {
                    return 'A senha deve ter no mínimo 6 caracteres';
                  }
                  return null;
                },
                onSaved: (value) {
                  _password = value!;
                },
              ),
              SizedBox(height: 20),
              ElevatedButton(
                onPressed: _saveForm,
                style: ElevatedButton.styleFrom(
                  foregroundColor: Colors.white,
                  backgroundColor: Colors.teal, // Cor do texto (branco)
                ),
                child: Text('Salvar'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}






















import 'package:flutter/material.dart';

class SuccessScreen extends StatelessWidget {
  final String name;
  final String lastName;
  final String email;
  final String password;

  SuccessScreen({
    required this.name,
    required this.lastName,
    required this.email,
    required this.password,
  });

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Dados do Usuário', style: TextStyle(color: Colors.white)),
        backgroundColor: Colors.teal, 
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Card(
          elevation: 4,
          child: Padding(
            padding: const EdgeInsets.all(16.0),
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                Text('Nome: $name', style: TextStyle(fontSize: 18)),
                SizedBox(height: 8),
                Text('Sobrenome: $lastName', style: TextStyle(fontSize: 18)),
                SizedBox(height: 8),
                Text('Email: $email', style: TextStyle(fontSize: 18)),
                SizedBox(height: 8),
                Text('Senha: $password', style: TextStyle(fontSize: 18)),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
























import 'package:flutter/material.dart';
import 'package:nome_do_projeto/forms_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Form App',
      theme: ThemeData(
        primarySwatch: Colors.teal,
        scaffoldBackgroundColor: Colors.grey[200],
      ),
      home: FormScreen(),
      debugShowCheckedModeBanner: false,
    );
  }
}
