# 10
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

// Simulating a screen like "PostScreen" from Firebase example
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Firebase Simulated App',
      home: PostScreen(),
      debugShowCheckedModeBanner: false,
    );
  }
}

class PostScreen extends StatefulWidget {
  @override
  _PostScreenState createState() => _PostScreenState();
}

class _PostScreenState extends State<PostScreen> {
  final TextEditingController titleController = TextEditingController();
  final TextEditingController contentController = TextEditingController();

  // Simulated Firebase Firestore using a list of maps
  List<Map<String, String>> posts = [];

  void addPost() {
    final title = titleController.text.trim();
    final content = contentController.text.trim();

    if (title.isNotEmpty && content.isNotEmpty) {
      setState(() {
        posts.add({
          'title': title,
          'content': content,
        });
        titleController.clear();
        contentController.clear();
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Simulated Firebase Posts'),
        backgroundColor: Colors.purple,
      ),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            // Input Fields
            TextField(
              controller: titleController,
              decoration: InputDecoration(labelText: 'Enter Title'),
            ),
            TextField(
              controller: contentController,
              decoration: InputDecoration(labelText: 'Enter Content'),
            ),
            SizedBox(height: 12),
            ElevatedButton(
              onPressed: addPost,
              child: Text('Add Post'),
              style: ElevatedButton.styleFrom(
                backgroundColor: Colors.purple,
              ),
            ),
            SizedBox(height: 20),
            Text(
              'All Posts',
              style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold),
            ),
            Divider(),
            // Displaying Posts
            Expanded(
              child: posts.isEmpty
                  ? Center(child: Text('No posts added yet.'))
                  : ListView.builder(
                      itemCount: posts.length,
                      itemBuilder: (context, index) {
                        return ListTile(
                          leading: Icon(Icons.message),
                          title: Text(posts[index]['title']!),
                          subtitle: Text(posts[index]['content']!),
                        );
                      },
                    ),
            ),
          ],
        ),
      ),
    );
  }
}
