# test

Movie Tickets file 






public class MovieTickets {

    private String movieName;
    private String screenNumber;
    private int noOfTickets;
    private String mobileNumber;
    private String time;
    private String modeOfPayment;

    public String getMovieName() {
        return movieName;
    }

    public void setMovieName(String movieName) {
        this.movieName = movieName;
    }

    public String getScreenNumber() {
        return screenNumber;
    }

    public void setScreenNumber(String screenNumber) {
        this.screenNumber = screenNumber;
    }

    public int getNoOfTickets() {
        return noOfTickets;
    }

    public void setNoOfTickets(int noOfTickets) {
        this.noOfTickets = noOfTickets;
    }

    public String getMobileNumber() {
        return mobileNumber;
    }

    public void setMobileNumber(String mobileNumber) {
        this.mobileNumber = mobileNumber;
    }

    public String getTime() {
        return time;
    }

    public void setTime(String time) {
        this.time = time;
    }

    public String getModeOfPayment() {
        return modeOfPayment;
    }

    public void setModeOfPayment(String modeOfPayment) {
        this.modeOfPayment = modeOfPayment;
    }

    public MovieTickets() {
    }

    public MovieTickets(String movieName, String screenNumber, int noOfTickets, String mobileNumber, String time, String modeOfPayment) {
        this.movieName = movieName;
        this.screenNumber = screenNumber;
        this.noOfTickets = noOfTickets;
        this.mobileNumber = mobileNumber;
        this.time = time;
        this.modeOfPayment = modeOfPayment;
    }

    public double calculatePrice() {
        // Fill in the code to calculate the total price based on screen number and number of tickets
        double ticketPrice = 0.0;
        double convenienceCharge = 0.0;
        
        // Determine ticket price based on screen number
        switch (screenNumber) {
            case "S1":
                ticketPrice = 280.0;
                convenienceCharge = 35.0;
                break;
            case "S2":
                ticketPrice = 250.0;
                convenienceCharge = 35.0;
                break;
            case "S3":
                ticketPrice = 520.0;
                convenienceCharge = 35.0;
                break;
            case "S4":
                ticketPrice = 400.0;
                convenienceCharge = 35.0;
                break;
            case "S5":
                ticketPrice = 180.0;
                break;
            default:
                break;
        }
        
        if (ticketPrice == 0.0) {
            return -1.0; // Invalid screen number
        }
        
        double totalPrice = noOfTickets * ticketPrice + convenienceCharge;
        return totalPrice;
    }

    public String generateTicketId() {
        // Fill in the code to generate the ticket ID
        if (screenNumber.length() != 2 || noOfTickets <= 0) {
            return "Invalid movie details";
        }

        String firstTwoConsonants = getFirstTwoConsonants(movieName);
        String ticketId = firstTwoConsonants + screenNumber + "N" + noOfTickets;
        return ticketId;
    }

    private String getFirstTwoConsonants(String str) {
        StringBuilder consonants = new StringBuilder();
        for (char c : str.toCharArray()) {
            if (Character.isLetter(c) && "AEIOUaeiou".indexOf(c) == -1) {
                consonants.append(c);
            }
            if (consonants.length() == 2) {
                break;
            }
        }
        return consonants.toString();
    }
}












User Interface

import java.util.Scanner;

public class UserInterface {
    
    public static MovieTickets extractDetails(String movieDetails) {
        // Split the movieDetails string by ":" and create a MovieTickets object
        String[] detailsArray = movieDetails.split(":");
        if (detailsArray.length != 6) {
            return null; // Invalid input format
        }
        
        String movieName = detailsArray[0];
        String screenNumber = detailsArray[1];
        int noOfTickets = Integer.parseInt(detailsArray[2]);
        String mobileNumber = detailsArray[3];
        String time = detailsArray[4];
        String modeOfPayment = detailsArray[5];
        
        return new MovieTickets(movieName, screenNumber, noOfTickets, mobileNumber, time, modeOfPayment);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        System.out.println("Enter the details");
        String movieDetails = sc.nextLine();
        
        MovieTickets ticket = extractDetails(movieDetails);
        
        if (ticket == null) {
            System.out.println("Invalid movie details");
        } else {
            System.out.println("Ticket Details");
            System.out.println("Movie Name: " + ticket.getMovieName());
            System.out.println("Screen Number: " + ticket.getScreenNumber());
            System.out.println("Number of tickets: " + ticket.getNoOfTickets());
            System.out.println("Show Timing: " + ticket.getTime());
            
            double totalPrice = ticket.calculatePrice();
            if (totalPrice < 0) {
                System.out.println("Invalid movie details");
            } else {
                System.out.println("Ticket Cost: " + totalPrice);
                System.out.println("Ticket ID: " + ticket.generateTicketId());
            }
        }
        
        sc.close();
    }
}
