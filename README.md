import javafx.application.Application;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.GridPane;
import javafx.stage.Stage;

import java.util.Optional;

public class main extends Application {

    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        primaryStage.setTitle("Aplikasi Pencatatan Tugas");

        // Buat komponen GUI
        Label label = new Label("Daftar Tugas:");
        ListView<String> taskListView = new ListView<>();
        Button addButton = new Button("Tambah");
        Button deleteButton = new Button("Hapus");

        // Set handler untuk tombol-tombol
        addButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                // Tampilkan dialog input untuk nama tugas
                TextInputDialog dialog = new TextInputDialog();
                dialog.setTitle("Tambah Tugas");
                dialog.setHeaderText(null);
                dialog.setContentText("Masukkan nama tugas:");

                // Dapatkan hasil input dari dialog
                Optional<String> result = dialog.showAndWait();
                result.ifPresent(taskName -> {
                    // Tambahkan tugas ke taskListView
                    taskListView.getItems().add(taskName);
                });
            }
        });

        deleteButton.setOnAction(new EventHandler<ActionEvent>() {
            @Override
            public void handle(ActionEvent event) {
                // Implementasi penghapusan tugas
                // Misalnya, hapus tugas yang dipilih
                int selectedIndex = taskListView.getSelectionModel().getSelectedIndex();
                if (selectedIndex != -1) {
                    taskListView.getItems().remove(selectedIndex);
                }
            }
        });

        // Set layout manager dan atur komponen GUI di dalamnya
        GridPane gridPane = new GridPane();
        
        gridPane.setPadding(new Insets(10, 10, 10, 10));
        gridPane.setVgap(8);
        gridPane.setHgap(10);

        GridPane.setConstraints(label, 0, 0);
        GridPane.setConstraints(taskListView, 0, 1, 2, 1);
        GridPane.setConstraints(addButton, 0, 2);
        GridPane.setConstraints(deleteButton, 1, 2);

        gridPane.getChildren().addAll(label, taskListView, addButton, deleteButton);

        // Set scene
        Scene scene = new Scene(gridPane, 300, 200);

        // Set stage dengan scene
        primaryStage.setScene(scene);

        // Tampilkan stage
        primaryStage.show();
    }
}
