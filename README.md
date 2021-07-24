package com.company;

import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Logic logic = new Logic();


        // Adding players, later I will do with wjile loop so it can be dynamic
        logic.textPlayersA();
        int amountOfPlayersA = sc.nextInt();
        int amountA = logic.amountOfPlayersA(amountOfPlayersA);
        TeamA tA = new TeamA(amountA);
        logic.enterPlayerName();
        String playersNameA = sc.nextLine();
        logic.addPlayerA(playersNameA,tA, amountOfPlayersA);
        //////////////////////////////////
        logic.textPlayersB();
        int amountOfPlayersB = sc.nextInt();
        int amountB = logic.amountOfPlayersB(amountOfPlayersB);
        TeamB tB = new TeamB(amountB);
        logic.enterPlayerName();
        String playersNameB = sc.nextLine();
        logic.addPlayerB(playersNameB,tB, amountOfPlayersB);

        //getting both team players printed
        tA.getPlayers();
        tB.getPlayers();
        System.out.println("________________________________________________");

        // checking that teams  are even regardless the amount of space in memory
        int totalPlayersA = tA.amountOfPlayers();
        int totalPlayersB = tB.amountOfPlayers();
        logic.compareAmountOfmembers(totalPlayersA, totalPlayersB);

        //who start guessing, the team with biggest number start choosing
        System.out.println("________________________________________________");
        int b = tA.startGuessing();
        int c = tB.startGuessing();
        logic.biggerNumberStart(b, c);

        // card with the letters is assingned
        System.out.println("________________________________________________");
        String playerA = tA.AssingCardsPlayer1(1);
        logic.assignCardsToLettersA(b, c, playerA, tA, amountOfPlayersA);
        String playerB = tB.AssingCardsPlayer1(1);
        logic.assignCardsToLettersB(b, c, playerB, tB, amountOfPlayersB);
    }
}
////////////////////////////////////////////////////////////////////////////////
package com.company;

import java.util.Scanner;


public class Logic {
    DealCards cardMeaning = new DealCards();
    Guess guess = new Guess();

    private String wth = cardMeaning.wth(); String lalaland = cardMeaning.lalaland(); String mma = cardMeaning.mma(); String ww2 = cardMeaning.ww2();
    String rt = cardMeaning.rt(); String ftp = cardMeaning.ftp();

    public void textPlayersA(){
        System.out.println("enter amount of players for team A");
    }
    public void textPlayersB(){
        System.out.println("enter amount of players for team B");
    }
    public void enterPlayerName(){System.out.println("enter players name");}
    public int amountOfPlayersA(int players){
        return players;
    }
    public int amountOfPlayersB(int players){
        return players;
    }
    public void compareAmountOfmembers(int x, int y){
        if (x != y){
            System.out.println("teams are not even");
            System.out.println("add more players");
            System.exit(0);
        }
        System.out.println("Team A have\t"+x+"\tmembers");
        System.out.println("Team B have\t"+y+"\tmembers");
    }
    public void biggerNumberStart(int x, int y){
        String winnerNumber = (x>y) ? "highest number is\t"+x : "highest number is\t"+y;
        System.out.println(winnerNumber);
    }
    public void addPlayerA(String player, TeamA tA, int amountOfpPlayers){
        Scanner sc =new Scanner(System.in);
        int count=0;
        do{
            System.out.println("insert players");
            player = sc.nextLine();
            tA.addPlayer(player);
            count++;
        }while(count < amountOfpPlayers);

    }
    public void addPlayerB(String player, TeamB tB, int amountOfpPlayers){
        Scanner sc =new Scanner(System.in);
        int count=0;
        do{
            System.out.println("insert players");
            player = sc.nextLine();
            tB.addPlayer(player);
            count++;
        }while(count < amountOfpPlayers);

    }
    public void assignCardsToLettersA(int b, int c, String playerA, TeamA tA, int amountOfPlayersA){
        int counter = 0;
        String hint ="";
        if(b>c){
            playerA = tA.AssingCardsPlayer1(1);
            String assignedCard = tA.assignedCard();
            if (assignedCard.contains("WW2")){
                assignedCard= ww2;
                hint = "war";
            }
            if (assignedCard.contains("MMA")){
                assignedCard= mma;
                hint = "fight";
            }
            if (assignedCard == "LALALAND"){
                assignedCard= lalaland;
                hint = "movie";
            }
            if (assignedCard == "RT"){
                assignedCard= rt;
                hint = "broadcasting";
            }
            if (assignedCard == "WTH"){
                assignedCard=wth;
                hint = "slang";
            }
            if (assignedCard == "FTP"){
                assignedCard= ftp;
                hint = "networking";
            }
            System.out.println("playerA is\t"+playerA);
            System.out.println("assigned card is\t"+tA.assignedCard());
            System.out.println("hint: "+hint);
            System.out.println("________________________________________________");
            String finalAssignedCard = assignedCard;
                    algoA(counter, amountOfPlayersA, tA, finalAssignedCard);
        }
    }
    public void assignCardsToLettersB(int b, int c, String playerB, TeamB tB, int amountOfPlayersB){
        int counter = 0;
        String hint = "";
        if(b<c){
            playerB = tB.AssingCardsPlayer1(1);
            String assignedCard = tB.assignedCard();
            if (assignedCard.contains("WW2")){
                assignedCard= ww2;
                hint = "war";
            }
            if (assignedCard.contains("MMA")){
                assignedCard= mma;
                hint = "fight";
            }
            if (assignedCard == "LALALAND"){
                assignedCard= lalaland;
                hint = "movie";
            }
            if (assignedCard == "RT"){
                assignedCard= rt;
                hint = "broadcasting";
            }
            if (assignedCard == "WTH"){
                assignedCard=wth;
                hint = "slang";
            }
            if (assignedCard == "FTP"){
                assignedCard= ftp;
                hint = "networking";
            }
            System.out.println("playerA is\t"+playerB);
            System.out.println("assigned card is\t"+tB.assignedCard());
            System.out.println("hint: "+hint);
            System.out.println("________________________________________________");

            algoB(counter, amountOfPlayersB, tB, assignedCard);
        }
    }

    public void algoA(int counter, int amountOfPlayersA,TeamA tA, String assignedCard){
        while(counter<amountOfPlayersA) {
            counter = 0;
            String playerName = tA.playerTurn(counter);
            System.out.println(counter);
                System.out.println("first player choice\t" + playerName);
                System.out.println("enter word");
                String word = guess.myScanner();
                String myWord = guess.myGuess(word);
                     if (myWord.equals(assignedCard)) {
                        System.out.println("you won");
                        break;
                        } else {
                    System.out.println("Next Player");
                     }
            counter++;
        }
    }
    public void algoB(int counter, int amountOfPlayersB,TeamB tB, String assignedCard){
        while(counter<amountOfPlayersB){
            counter = 0;
            String playerName = tB.playerTurn(counter);
            System.out.println(counter);
            System.out.println("first player choice\t"+playerName);
            System.out.println("enter word");
            String word = guess.myScanner();
            String myWord = guess.myGuess(word);
            if(myWord.equals(assignedCard)){
                System.out.println("you won");
                break;
            }else{
                System.out.println("Next Player");
            }
            counter++;
        }
    }

}

//////////////////////////////////////////////////////////////////////////////////
package com.company;

import java.util.ArrayList;
import java.util.Collections;


public class DealCards {
    //These are supposed to be the cards
   private String a = "WW2";String b = "MMA";String c = "LALALAND";
            String d = "RT";String f = "WTH";String g = "FTP";

    public String ww2(){
       String a = "war world 2";
       return a;
   }
    public String mma(){
        String b = "mixed martial arts";
        return b;
    }
    public String lalaland(){
        String c = "la la land";
        return c;
    }
    public String rt(){
        String d = "radio tv";
        return d;
    }
    public String wth(){
        String f = "what the hell";
        return f;
    }
    public String ftp(){
        String g = "file transfer protocol";
        return g;
    }

    //Cards are stored in this arrayList
    ArrayList<String> cards = new ArrayList<String>();

    // Here Cards are shuffle so user dont sam ecards everytime.
    ArrayList<String> cards(){
        cards.add(a);
        cards.add(b);
        cards.add(c);
        cards.add(d);
        cards.add(f);
        cards.add(g);
        Collections.shuffle(cards);
        return cards;
    }

}
/////////////////////////////////////////////////////////////////////////////////////
package com.company;

import java.util.Scanner;

public  class  Guess {
    public String myGuess(String word){
        return word;
    }
    public String myScanner(){
        Scanner sc = new Scanner(System.in);
        String word = sc.nextLine();
        return word;
    }

}
/////////////////////////////////////////////////////////////////////////
package com.company;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Random;

public class TeamA implements TeamsFeatures {
    String[] team;
    int counter;
    DealCards dealCards = new DealCards();
    ArrayList c = dealCards.cards();

    //Setting amount of players in team in dynamic array
    public TeamA(int amountOfPlayers) {
        team = new String[amountOfPlayers];
    }

    //Adding players to Array, if Array is filled it automatically generates more space in memory
    public void addPlayer(String newPlayer) {
        if (team.length == counter) {
            String[] teamResize = new String[counter * 2];
            for (int i = 0; i < counter; i++)
                teamResize[i] = team[i];
            team = teamResize;
        }
        team[counter++] = newPlayer;
    }

    //printing all players if needed
    @Override
    public void getPlayers() {
        for (int i = 0; i < counter; i++) {
        }
        System.out.println(Arrays.toString(team));
    }
    @Override
    public String playerTurn(int position){
        for (int i = 0; i < counter; i++) {
        }
        return team[position];
    }

    // Assign cards to players
    @Override
    public String AssingCardsPlayer1(int position) {
        for (int i = 0; i < counter; i++) {
        }
            return team[position];
    }

    // Assigned card
    @Override
    public String assignedCard(){
        String x = (String) c.get(0);
        return x;
    }

    @Override
    //Checking amount of players and compare to the other team. both should be equal
    public int amountOfPlayers() {
        int x = 0;
        for (int i = 0; i < counter; i++) {
            if (team[i] == null)
                break;
                x = i;
        }
        return x+1;
    }

    //team with biggest number start guessing
    @Override
    public int startGuessing(){
        Random rand = new Random();
        int number = rand.nextInt(10);
        return number;
    }
}
/////////////////////////////////////////////////
package com.company;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Random;

public class TeamB implements TeamsFeatures {
    String[] team;
    int counter;
    DealCards dealCards = new DealCards();
    ArrayList c = dealCards.cards();

    public TeamB(int amountOfPlayers) {
        team = new String[amountOfPlayers];
    }
    public void addPlayer(String newPlayer){
        if(team.length==counter){
            String[] teamResize = new String[counter*2];
            for (int i = 0; i < counter; i++)
                teamResize[i] = team[i];
            team = teamResize;
        }
        team[counter++]=newPlayer;
    }

    @Override
    public void getPlayers() {
        for (int i = 0; i < counter; i++) {
        }System.out.println(Arrays.toString(team));
    }

    @Override
    public String AssingCardsPlayer1(int position) {
        for (int i = 0; i < counter; i++) {
        }
        return team[position];
    }
    @Override
    public String assignedCard(){
        String x = (String) c.get(0);
        return x;
    }

    @Override
    public String playerTurn(int position) {
        for (int i = 0; i < counter; i++) {
        }
        return team[position];
    }

    @Override
    public int amountOfPlayers() {
        int x = 0;
        for (int i = 0; i < counter; i++) {
            if (team[i] == null)
                break;
            x = i;
        }
        return x+1;
    }

    @Override
    public int startGuessing() {
        Random rand = new Random();
        int number = rand.nextInt(10);
        return number;
    }
}
/////////////////////////////////////////////////////////////
package com.company;

public interface TeamsFeatures {
     void getPlayers();
     String AssingCardsPlayer1(int position);
     String assignedCard();
     String playerTurn(int position);
     int amountOfPlayers();
     int startGuessing();
}
