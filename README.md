# WeathreApp
MICRO IT INTERNSHIP PROJECT 1: WEATHERAPP

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import java.util.Scanner;

public class WeatherApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter city name: ");
        String city = scanner.nextLine();
        
        // Replace with your actual API key
        String apiKey = "YOUR_API_KEY_HERE";
        String urlString = "https://api.openweathermap.org/data/2.5/weather?q=" 
                            + city + "&units=metric&appid=" + apiKey;

        try {
            URL url = new URL(urlString);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();
            conn.setRequestMethod("GET");

            int responseCode = conn.getResponseCode();

            if (responseCode == 200) {
                BufferedReader reader = new BufferedReader(
                        new InputStreamReader(conn.getInputStream()));
                StringBuilder response = new StringBuilder();
                String line;

                while ((line = reader.readLine()) != null) {
                    response.append(line);
                }
                reader.close();

                System.out.println("\nWeather Data:");
                System.out.println(response.toString());  // Raw JSON response
            } else {
                System.out.println("Error: City not found or API call failed.");
            }

        } catch (Exception e) {
            System.out.println("Exception occurred: " + e.getMessage());
        }
    }
}
