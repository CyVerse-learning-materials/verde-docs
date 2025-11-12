# Chatbox AI

Chatbox AI is a cross-platform desktop and mobile application that allows you to interact with AI-VERDE models through an intuitive chat interface. It runs on **Windows, macOS, Linux, Android, iOS, and Web**.

This will guide you through connecting your AI-VERDE API Key, configuring your models, and starting your first conversation.

## Prerequisites

1. **AI-VERDE API Key and API URL**  
   - Obtain your credentials by following the [AI-VERDE API Token Guide](api-token.md).  

2. **Model Information**  
   - Review the models you plan to use in the [AI-VERDE Model Documentation](api-key-models.md).  

3. **Chatbox AI Installation**  
   - Download the installer for your operating system from the [Chatbox AI Download Page](https://chatboxai.app/en#download).  

4. **Terminal or Application Access**  
   - These instructions assume **Chatbox AI** is already installed and accessible on your system.


## 1. Configure AI-VERDE in Chatbox AI

Follow these steps to connect Chatbox AI with your AI-VERDE account:

1. Launch Chatbox AI
2. Click "Settings" in the sidebar or top menu  
3. Select "Model Provider"
4. Click "+ Add" button
   &nbsp;
   ![chatbox ai](../assets/chatboxai01.png){: style="width:95%"}  
   &nbsp;
5. In the Name field, enter "AI-VERDE"  
6. Leave API Mode set to "OpenAI API Compatible"  
7. Click "Add"
   &nbsp;  
   ![chatbox ai](../assets/chatboxai02.png){: style="width:80%"}  
   &nbsp;
You should now see the AI-VERDE configuration panel on the right.
1. Enter (or paste) your AI-VERDE API Key into the API Key field  
2. Enter (or paste) your AI-VERDE API URL into the API Host field 
   &nbsp; 
   ![chatbox ai](../assets/chatboxai03.png){: style="width:80%"}  
   &nbsp; 
3.  In the Model section, click "New" to open a new model dialog  
4.  Enter the "Model ID" (this corresponds to the `"id"` value from your model list)  
5.  Under capabilities, select options such as *Vision*, *Reasoning*, or *Tool Use* if your model supports them. Note: *Capabilities for a model can be modified later.*  
6.  Click "Save"  
    &nbsp; 
    ![chatbox ai](../assets/chatboxai04.png){: style="width:80%"} 
    &nbsp;  
7.  (Optional) Repeat steps 10–13 to add additional models  
8.  Click "Check" to test your connection to AI-VERDE  

If the test passes, your setup is complete — you’re ready to chat!

## 2. Using Chatbox AI with Configured Models

Once your models are set up, chatting is simple:

1. Click "New Chat" or select a past conversation from the left panel  
2. Choose the model you want to use for this chat session
   &nbsp;
   ![chatbox ai](../assets/chatboxai05.png){: style="width:95%"}
   &nbsp;
3. Type your question or request in the chat box and press "Enter".

That’s it! You’re now chatting directly with your configured AI-VERDE model.

### Explore More

Chatbox AI includes many advanced features — conversation history, model switching, plugin support, and more. Feel free to explore the interface and discover what works best for your workflow.