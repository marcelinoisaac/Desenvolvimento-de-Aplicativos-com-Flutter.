import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: IMCCalculator(),
    debugShowCheckedModeBanner: false,
  ));
}

class IMCCalculator extends StatefulWidget {
  @override
  _IMCCalculatorState createState() => _IMCCalculatorState();
}

class _IMCCalculatorState extends State<IMCCalculator> {
  // Controladores para peso e altura
  TextEditingController weightController = TextEditingController();
  TextEditingController heightController = TextEditingController();
  String _resultado = "Informe seus dados";

  // Função para limpar os campos
  void _reset() {
    weightController.text = "";
    heightController.text = "";
    setState(() {
      _resultado = "Informe seus dados";
    });
  }

  // Calculo do IMC
  void _calculateIMC() {
    setState(() {
      double peso = double.parse(weightController.text.replaceAll(',', '.'));
      double altura = double.parse(heightController.text.replaceAll(',', '.'));
      double imc = peso / (altura * altura);

      if (imc < 18.5) {
        _resultado = "IMC: ${imc.toStringAsFixed(2)} (Abaixo do peso)";
      } else if (imc >= 18.5 && imc < 24.9) {
        _resultado = "IMC: ${imc.toStringAsFixed(2)} (Peso normal)";
      } else if (imc >= 25 && imc < 29.9) {
        _resultado = "IMC: ${imc.toStringAsFixed(2)} (Sobrepeso)";
      } else {
        _resultado = "IMC: ${imc.toStringAsFixed(2)} (Obesidade)";
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text(
          "Calculadora de IMC",
          style: TextStyle(color: Colors.white),
        ),
        centerTitle: true,
        backgroundColor: Colors.blueAccent,
        actions: <Widget>[
          IconButton(
              icon: Icon(Icons.refresh, color: Colors.white),
              onPressed: () {
                _reset();
              })
        ],
      ),
      body: SingleChildScrollView(
        padding: EdgeInsets.fromLTRB(10.0, 0, 10.0, 0),
        child: Form(
          child: Column(
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: <Widget>[
              Icon(
                Icons.person,
                size: 150.0,
                color: Colors.blueAccent,
              ),
              TextField(
                controller: weightController,
                textAlign: TextAlign.center,
                keyboardType: TextInputType.number,
                decoration: InputDecoration(
                    labelText: "Peso em Kg",
                    labelStyle: TextStyle(color: Colors.blueAccent)),
                style: TextStyle(color: Colors.blueAccent, fontSize: 26.0),
              ),
              TextField(
                controller: heightController,
                textAlign: TextAlign.center,
                keyboardType: TextInputType.number,
                decoration: InputDecoration(
                    labelText: "Altura em metros",
                    labelStyle: TextStyle(color: Colors.blueAccent)),
                style: TextStyle(color: Colors.blueAccent, fontSize: 26.0),
              ),
              Padding(
                padding: EdgeInsets.only(top: 20.0, bottom: 20.0),
                child: Container(
                  height: 50.0,
                  child: ElevatedButton(
                    child: Text("Calcular",
                        style: TextStyle(color: Colors.white, fontSize: 26.0)),
                    style: ElevatedButton.styleFrom(
                        backgroundColor: Colors.blueAccent),
                    onPressed: () {
                      _calculateIMC();
                    },
                  ),
                ),
              ),
              Text(
                _resultado,
                textAlign: TextAlign.center,
                style: TextStyle(color: Colors.blueAccent, fontSize: 26.0),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
