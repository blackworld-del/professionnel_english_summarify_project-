### Introduction

> **Purpose of the Document**

	This document serves as a guide for stakeholders, developers, 
	and testers involved in the Summarify project. 
	It details the application overview, user interface design, working 
	of Summarify and potential future enhancements of our application.

> **Overview of the Mobile App**

	Summarify is a mobile application designed to assist users in
	summarizing lengthy texts using BART algorithms. BART is a Large 
	Language Model algorithm which designed for sequence-to-sequence tasks
	with a particular focus on text generation and summarization. 
	By leveraging state-of-the-art natural language processing techniques, 
	the app provides users with concise and coherent summaries of input text, 
	streamlining information consumption.

## Installation

> Thank you for your interest in Summarify  the text summarization app designed exclusively for Android users. While the app is not currently available for installation, we're diligently working to bring you an exceptional experience on the Android platform.

**Developers Installation Guide**

## flutter version : 

```java
Flutter : 3.16.0
```

- Clone the Repository:

Clone the Summarify Beta repository using the following command in your terminal:

```ruby
git clone https://github.com/summarify/beta.git
```

- Navigate to the Project Directory:
  
```ruby
cd lib
```
## open the pubsec.yaml and install all the dependecies : 

```java
cupertino_icons: ^1.0.2
build_runner: ^2.4.7
dio: ^5.3.4
fluentui_system_icons: ^1.1.222
flutter_lints: ^2.0.0
gap: ^3.0.1
hexcolor: ^3.0.1
hive_flutter: ^1.1.0
hive_generator: ^2.0.1
salomon_bottom_bar: ^3.3.2
```

- open terminal window in the **main** file and run this command:
  
```ruby
flutter run --v
```

## User Interface : 

> Overview :

Summarify features a straightforward and user-friendly interface, designed to facilitate a seamless experience for users engaging in text summarization. This section provides insights into the key screens of the app.

```diff
@@ Home Screen : @@
```

> The home screen acts as a central hub, presenting users with an organized view of all previously saved texts.

- **Saved Texts List :**

1 .Displays a list of all texts previously saved by the user.
2 .button for creating new process for summarize

- **Navigation Bar :**

Provides quick access to other screens, including the text profile screen and search screen.

```diff
@@ Text Input Screen : @@
```
> This screen allows users to input text for summarization and view the generated result.

- **Input Text Field :**

Allows users to input or paste the text they wish to summarize.

- **Summarize Button :**

Initiates the text summarization process

- **Generated Summary :**

Displays the summarized text produced by the BART algorithm.

- **Svae Button :**

  button for saving the result from the api response

## Text Summarization Process :

> How it Works :

The text summarization process within Summarify involves leveraging BART algorithms. BART, being a state-of-the-art Large Language Model, excels in sequence-to-sequence tasks, making it ideal for text summarization. The app breaks down the summarization process into the following steps:

- **Input Text Processing :**

The user-provided text undergoes preprocessing to enhance the efficiency of the summarization algorithm.

- **BART Algorithm Execution :**

The processed text is fed into the BART algorithm using the llm api from huggingface, which generates a coherent summary.

- **Summary Presentation :**

The generated summary is presented to the user on the summary screen.

- **API Integration Code :**

> Overview :

The following code snippet demonstrates how Summarify integrates with the Language Model API (LLM API) for text summarization.

```diff
! makeRequest Function : 
```
The **makeRequest** function is responsible for making requests to the LLM API and handling the responses.

```dart
import 'package:dio/dio.dart';
import 'dart:convert';

/// Makes a request to the Language Model API (LLM API) for text summarization.
///
/// Parameters:
///   - llmText: The input text to be summarized.
///
/// Returns:
///   - A Dio [Response] object containing the API response.
Future<Response> makeRequest({
  required String llmText,
}) async {
  Dio dio = Dio();
  var url = 'https://proeng.dadahoualid.repl.co/query';
  var data = {
    'inputs': llmText,
  };

  try {
    Response response = await dio.post(
      url,
      data: jsonEncode(data),
      options: Options(
        headers: {
          'Content-Type': 'application/json; charset=UTF-8',
        },
      ),
    );

    return response;
  } catch (error) {
    // Handle any potential errors during the API request.
    print('Error during API request: $error');
    throw error;
  }
}

```
