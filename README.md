It is a mathGame. That will add Random question.Which You have to answer and you will get point .
there using javafx code 
package com.example.mathgame;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;
import java.util.Random;

public class GameUI extends Application {
    private int correctAnswers = 0;

    @Override
    public void start(Stage primaryStage) {
        Random random = new Random();
        Label questionLabel = new Label();
        TextField answerField = new TextField();
        Button submitButton = new Button("Submit");
        Label feedbackLabel = new Label();
        Label scoreLabel = new Label("Score: 0");

        // Generate a random math question
        generateQuestion(random, questionLabel);

        // Set up the submit button event
        submitButton.setOnAction(event -> {
            int correctAnswer = (int) questionLabel.getUserData();
            try {
                int userAnswer = Integer.parseInt(answerField.getText());
                if (userAnswer == correctAnswer) {
                    correctAnswers++;
                    feedbackLabel.setText("Correct!");
                } else {
                    feedbackLabel.setText("Wrong!");
                }
                scoreLabel.setText("Score: " + correctAnswers);
                generateQuestion(random, questionLabel);
                answerField.setText("");
            } catch (NumberFormatException e) {
                feedbackLabel.setText("Please enter a valid number.");
            }
        });

        VBox layout = new VBox(10, questionLabel, answerField, submitButton, feedbackLabel, scoreLabel);
        Scene scene = new Scene(layout, 300, 200);

        primaryStage.setTitle("Math Magic");
        primaryStage.setScene(scene);
        primaryStage.show();
    }

    private void generateQuestion(Random random, Label questionLabel) {
        int num1 = random.nextInt(10) + 1;  // Numbers 1-10
        int num2 = random.nextInt(10) + 1;
        int operation = random.nextInt(3);  // 0=addition, 1=subtraction, 2=multiplication

        String question;
        int answer;
        switch (operation) {
            case 0:
                question = num1 + " + " + num2;
                answer = num1 + num2;
                break;
            case 1:
                question = num1 + " - " + num2;
                answer = num1 - num2;
                break;
            default:
                question = num1 + " * " + num2;
                answer = num1 * num2;
                break;
        }
        questionLabel.setText(question + " = ?");
        questionLabel.setUserData(answer); // Store the answer in the label's user data.
    }

    public static void main(String[] args) {
        launch(args);
    }
}
