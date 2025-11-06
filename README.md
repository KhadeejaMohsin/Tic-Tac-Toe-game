import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        char[][] board = {
            {' ', ' ', ' '},
            {' ', ' ', ' '},
            {' ', ' ', ' '}
        };

        char currentPlayer = 'X';
        Scanner scanner = new Scanner(System.in);

        while (true) {
            printBoard(board);
            System.out.println("Player " + currentPlayer + ", enter your move (row and column 1-3): ");
            
            int row = scanner.nextInt() - 1;
            int col = scanner.nextInt() - 1;

            // Check for valid move
            if (row < 0 || row >= 3 || col < 0 || col >= 3) {
                System.out.println("Invalid position! Try again.");
                continue;
            }

            if (board[row][col] != ' ') {
                System.out.println("That spot is already taken! Try again.");
                continue;
            }

            // Make the move
            board[row][col] = currentPlayer;

            // Check for win
            if (hasWon(board, currentPlayer)) {
                printBoard(board);
                System.out.println("🎉 Player " + currentPlayer + " wins!");
                break;
            }

            // Check for draw
            if (isBoardFull(board)) {
                printBoard(board);
                System.out.println("It's a draw!");
                break;
            }

            // Switch turns
            currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
        }

        scanner.close();
    }

    // Function to print the board
    public static void printBoard(char[][] board) {
        System.out.println("\n-------------");
        for (int i = 0; i < 3; i++) {
            System.out.print("| ");
            for (int j = 0; j < 3; j++) {
                System.out.print(board[i][j] + " | ");
            }
            System.out.println("\n-------------");
        }
    }

    // Function to check if a player has won
    public static boolean hasWon(char[][] board, char player) {
        // Check rows
        for (int i = 0; i < 3; i++) {
            if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
                return true;
        }

        // Check columns
        for (int i = 0; i < 3; i++) {
            if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
                return true;
        }

        // Check diagonals
        if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
            return true;

        if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
            return true;

        return false;
    }

    // Function to check for draw
    public static boolean isBoardFull(char[][] board) {
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (board[i][j] == ' ')
                    return false;
            }
        }
        return true;
    }
}
