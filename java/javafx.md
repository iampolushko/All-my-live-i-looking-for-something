### Save the file as

```java
 doneTestButton.setOnAction(actionEvent -> {
            FileChooser fileChooser = new FileChooser();

            //Set extension filter for text files
            FileChooser.ExtensionFilter extFilter = new FileChooser.ExtensionFilter("TXT files (*.txt)", "*.txt");
            fileChooser.getExtensionFilters().add(extFilter);

            //Show save file dialog
            File file = fileChooser.showSaveDialog((Stage) anchorPane.getScene().getWindow());

            if (file != null) {
                try {
                    PrintWriter writer;
                    writer = new PrintWriter(file);
                    writer.println("hello");
                    writer.close();
                } catch (IOException ex) {
                    Logger.getLogger(HelloController.class.getName()).log(Level.SEVERE, null, ex);
                }
            }
        });
```

### Page intent
