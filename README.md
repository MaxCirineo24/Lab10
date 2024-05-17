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
import 'package:google_fonts/google_fonts.dart';

void main() {
  runApp(ProductDetailApp());
}

class ProductDetailApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Product Detail',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ProductDetailScreen(),
    );
  }
}

class ProductDetailScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Product Detail'),
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
           Center(
              child: Image.asset(
                'assets/images/product.png',
                width: 200,
                height: 200,
              ),
            ),
            SizedBox(height: 16),
            Text(
              'Product Name',
              style: GoogleFonts.montserrat(
                textStyle: TextStyle(
                  fontSize: 24,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ),
            SizedBox(height: 8),
            Text(
              '\$99.99',
              style: GoogleFonts.roboto(
                textStyle: TextStyle(
                  fontSize: 20,
                  color: Colors.green,
                  fontWeight: FontWeight.w500,
                ),
              ),
            ),
            SizedBox(height: 16),
            Text(
              'This is a brief description of the product. It provides key details and features that make this product unique and desirable.',
              style: GoogleFonts.nunito(
                textStyle: TextStyle(
                  fontSize: 16,
                  color: Colors.black87,
                ),
              ),
            ),
          ],
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


