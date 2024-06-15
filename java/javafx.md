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

```java
    @FXML
    private Button submitButton;

    @FXML
    void initialize() throws SQLException {
        //Whole process of page intent
        submitButton.setOnAction(actionEvent -> {
            FXMLLoader loader = new FXMLLoader();
            loader.setLocation(getClass().getResource("main-view.fxml"));
            try {
                Stage stage = (Stage) submitButton.getScene().getWindow();
                stage.close();
                loader.load();
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
            Stage stage = new Stage();
            stage.setScene(new Scene(loader.getRoot()));
            stage.showAndWait();

        });

        Statement statement = DBHandler.createConnection();
        DBProduct dbProduct = new DBProduct(statement);
        System.out.println(dbProduct.getDbProduct());
    }
```
