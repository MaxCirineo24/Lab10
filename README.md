# Lab9


EJERCICIO 1
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

void main() {
  runApp(CategoryListApp());
}

class CategoryListApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Category List',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CategoryListScreen(),
    );
  }
}

class CategoryListScreen extends StatelessWidget {
  final List<CategoryItem> items = [
    CategoryItem(
      name: 'Apple',
      imagePath: 'assets/images/apple.png',
      category: 'food',
    ),
    CategoryItem(
      name: 'Dog',
      imagePath: 'assets/images/dog.png',
      category: 'animals',
    ),
    CategoryItem(
      name: 'Paris',
      imagePath: 'assets/images/paris.png',
      category: 'places',
    ),
    CategoryItem(
      name: 'Pizza',
      imagePath: 'https://example.com/pizza.jpg',
      category: 'food',
    ),
    CategoryItem(
      name: 'Cat',
      imagePath: 'https://example.com/cat.jpg',
      category: 'animals',
    ),
    CategoryItem(
      name: 'New York',
      imagePath: 'https://example.com/newyork.jpg',
      category: 'places',
    ),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Category List'),
      ),
      body: ListView.builder(
        itemCount: items.length,
        itemBuilder: (context, index) {
          return _buildCategoryItem(items[index]);
        },
      ),
    );
  }

  Widget _buildCategoryItem(CategoryItem item) {
    TextStyle textStyle;
    switch (item.category) {
      case 'food':
        textStyle = GoogleFonts.openSans(fontSize: 18, fontWeight: FontWeight.bold);
        break;
      case 'animals':
        textStyle = GoogleFonts.lato(fontSize: 18, fontWeight: FontWeight.bold);
        break;
      case 'places':
        textStyle = GoogleFonts.ubuntu(fontSize: 18, fontWeight: FontWeight.bold);
        break;
      default:
        textStyle = TextStyle(fontSize: 18, fontWeight: FontWeight.bold);
    }

    return Card(
      margin: EdgeInsets.symmetric(vertical: 10, horizontal: 16),
      child: ListTile(
        leading: item.imagePath.startsWith('http')
            ? Image.network(item.imagePath, width: 50, height: 50, fit: BoxFit.cover)
            : Image.asset(item.imagePath, width: 50, height: 50, fit: BoxFit.cover),
        title: Text(item.name, style: textStyle),
      ),
    );
  }
}

class CategoryItem {
  final String name;
  final String imagePath;
  final String category;

  CategoryItem({
    required this.name,
    required this.imagePath,
    required this.category,
  });
}



EJERCICIO 2

import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Producto(),
    );
  }
}

class Producto extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Detalles del Producto Max Cirineo'),
        centerTitle: true,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.center,
            children: [
              Image.asset(
                'assets/images/tabas.jpg',
                width: 200, // Ancho deseado
                height: 200, // Alto deseado
                fit: BoxFit.cover, // Ajuste de la imagen
              ),
              SizedBox(height: 20),
              Text(
                'Zapatillas Mike T-42',
                style: TextStyle(
                  fontFamily: 'Montserrat', // Corregir el nombre de la fuente
                  fontSize: 24,
                  fontWeight: FontWeight.bold,
                ),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 10),
              Text(
                '\$200.99', // Corregir el símbolo de dólar para que se muestre correctamente
                style: TextStyle(
                  fontFamily: 'Roboto',
                  fontSize: 18,
                  color: Colors.green, // Color del texto del precio
                ),
                textAlign: TextAlign.center,
              ),
              SizedBox(height: 20),
              Padding(
                padding: const EdgeInsets.symmetric(horizontal: 16.0),
                child: Text(
                  'Dale a tu look un toque fresco y vibrante con las nuevas zapatillas Mike AirMax VerdeBlanco. Diseñadas para aquellos que buscan comodidad sin sacrificar estilo, estas zapatillas combinan tecnología avanzada y un diseño moderno que te hará destacar.',
                  style: TextStyle(
                    fontFamily: 'Nunito',
                    fontSize: 16,
                  ),
                  textAlign: TextAlign.center,
                ),
              ),
            ],
          ),
        ),
      ),
    );
  }
}

EJERCICIO3

Flutter
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';
import 'package:google_fonts/google_fonts.dart';

void main() {
  runApp(GalleryApp());
}

class GalleryApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Image Gallery',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: GalleryScreen(),
    );
  }
}

class GalleryScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Gallery'),
      ),
      body: ListView(
        padding: EdgeInsets.all(8.0),
        children: [
          _buildImageCard('assets/images/pan.jpeg', 'pan.jpeg', GoogleFonts.merriweather(fontSize: 18)),
          _buildImageCard('assets/images/josua.png', 'josua.png', GoogleFonts.lato(fontSize: 18)),
          _buildImageCard('assets/images/amigo.svg', 'amigo.svg', GoogleFonts.roboto(fontSize: 18)),
        ],
      ),
    );
  }

  Widget _buildImageCard(String imagePath, String imageName, TextStyle textStyle) {
    Widget imageWidget;

    if (imagePath.endsWith('.svg')) {
      imageWidget = SvgPicture.asset(imagePath, width: 200, height: 200);
    } else {
      imageWidget = Image.asset(imagePath, width: 200, height: 200);
    }

    return Card(
      margin: EdgeInsets.symmetric(vertical: 10),
      child: Padding(
        padding: EdgeInsets.all(8.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            imageWidget,
            SizedBox(height: 8),
            Text(imageName, style: textStyle),
          ],
        ),
      ),
    );
  }
}


