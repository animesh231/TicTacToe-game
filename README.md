 import jdk.jfr.SettingControl;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

//public class MyNewGame {


    public class MyNewGame extends JFrame implements ActionListener {

        JLabel heading,clockLabel;
        JPanel mainpanel;



        // game instance variable.



        int []gameChances ={2,2,2,2,2,2,2,2,2};
        int activePlayer=0;

        // winning positions

        int wps[][] = {
                {0,1,2},
                {3,4,5},
                {6,7,8},
                {0,3,6},
                {1,4,7},
                {2,5,8},
                {0,4,8},
                {2,4,6}
        };
        int winner = 2;

        boolean gameover = false;


        Font font = new Font("",Font.BOLD,40);
        MyNewGame(){
            System.out.println("Creating Instance Of Game");
            setTitle ("My Tic Tac Toe Game..");
            setSize (850,850);
            ImageIcon icon = new ImageIcon("src/images/ticractoenewimage.png");

            setIconImage(icon.getImage());
            setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            createGUI();
            setVisible(true);

        }

        private void createGUI(){
            this.getContentPane().setBackground(Color.decode("#2196f3"));
            this.setLayout(new BorderLayout());

            // north heading

            heading = new JLabel("Tic Tac Toe");
            heading.setFont(font);
            heading.setHorizontalAlignment(SwingConstants.CENTER);
            heading.setForeground(Color.BLACK);

            this.add(heading,BorderLayout.NORTH);

            // JLabel creating object of clock
//
//        clockLabel = new JLabel("Clock");
//        clockLabel.setFont(font);
//        clockLabel.setHorizontalAlignment(SwingConstants.CENTER);
//        this.add(clockLabel,BorderLayout.SOUTH);

            /// panel section
            mainpanel =  new JPanel();
            mainpanel.setLayout(new GridLayout(3,3));
            for(int i = 1; i<=9; i++ ){
                JButton btn = new JButton();
                // btn.setIcon(new ImageIcon("src/img/0.png"));
                btn.setFont(font);
                btn.setBackground(Color.decode("#90caf9"));
                mainpanel.add(btn);
                this.add(mainpanel,BorderLayout.CENTER);
                btn.addActionListener(this);
                btn.setName(String.valueOf(i - 1));

            }
        }

        @Override
        public void actionPerformed(ActionEvent e) {
            System.out.println("Clicked");

            JButton currentButton = (JButton)e.getSource();

            String nameStr = currentButton.getName();

            int name = Integer.parseInt(nameStr.trim());

            if(gameover){

                JOptionPane.showMessageDialog(this, " Game already over ");
                return;
            }

            if (gameChances[name]==2)
            {
                if (activePlayer == 1)
                {
                    currentButton.setIcon(new ImageIcon("src/img/0.1.png"));


                    gameChances[name] = activePlayer;
                    activePlayer= 0;

                }else{
                    currentButton.setIcon(new ImageIcon("src/img/x.1.png"));


                    gameChances[name] = activePlayer;
                    activePlayer= 1;

                }



                for(int []temp:wps){

                    if(gameChances[temp[0]] == gameChances[temp[1]] && (gameChances[temp[1]]) == gameChances[temp[2]] && gameChances[temp[2]]!=2){

                        winner = gameChances[temp[1]];
                        gameover = true;

                        JOptionPane.showMessageDialog(null, "Player " + winner + " has won the match" );

                        int i = JOptionPane.showConfirmDialog(this, " Do you want to play more ");

                        if(i == 0 ){

                            this.setVisible(false);
                            new MyNewGame();

                        } else if (i == 1) {
                            System.exit(12345);

                        }else {

                        }
                        System.out.println(i);
                        break;

                    }
                }

                // Draw Logic............................


                int c = 0;
                for(int x: gameChances){
                    if(x == 2){
                        c++;
                        break;

                    }

                }
                if( c == 0 && gameover == false){
                    JOptionPane.showMessageDialog(null, "Its Draw.");
                    int i = JOptionPane.showConfirmDialog(this, " Play More ??");

                    if( i == 0 ){
                        this.setVisible(false);

                        new MyNewGame();

                    } else if (i == 1) {

                        System.exit(1212);

                    }else{

                    }

                    gameover = true;

                }


            } else{
                JOptionPane.showMessageDialog(this, "Position already occupied... ");
            }

        }



    }

