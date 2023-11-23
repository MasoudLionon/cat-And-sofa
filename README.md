# cat-And-sofa
game
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;

public class CatAndSofaGame extends JFrame implements ActionListener, KeyListener {
    private int catX = 50;
    private int catY = 50;
    private int sofaX = 200;
    private int sofaY = 200;

    public CatAndSofaGame() {
        setTitle("Cat and Sofa Game");
        setSize(400, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setResizable(false);

        Timer timer = new Timer(100, this);
        timer.start();

        addKeyListener(this);
        setFocusable(true);
        setFocusTraversalKeysEnabled(false);
    }

    public void actionPerformed(ActionEvent e) {
        checkCollision();
        repaint();
    }

    public void keyPressed(KeyEvent e) {
        int key = e.getKeyCode();

        if (key == KeyEvent.VK_LEFT) {
            catX -= 10;
        } else if (key == KeyEvent.VK_RIGHT) {
            catX += 10;
        } else if (key == KeyEvent.VK_UP) {
            catY -= 10;
        } else if (key == KeyEvent.VK_DOWN) {
            catY += 10;
        }

        checkCollision();
        repaint();
    }

    public void keyTyped(KeyEvent e) {
    }

    public void keyReleased(KeyEvent e) {
    }

    private void checkCollision() {
        if (catX < 0) {
            catX = 0;
        } else if (catX > getWidth() - 50) {
            catX = getWidth() - 50;
        }

        if (catY < 0) {
            catY = 0;
        } else if (catY > getHeight() - 50) {
            catY = getHeight() - 50;
        }

        if (catX < sofaX + 50 && catX + 50 > sofaX && catY < sofaY + 50 && catY + 50 > sofaY) {
            // Collision occurred, do something
            System.out.println("Cat caught the sofa!");
        }
    }

    public void paint(Graphics g) {
        super.paint(g);

        g.setColor(Color.BLUE);
        g.fillRect(catX, catY, 50, 50);

        g.setColor(Color.RED);
        g.fillRect(sofaX, sofaY, 50, 50);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            CatAndSofaGame game = new CatAndSofaGame();
            game.setVisible(true);
        });
    }
}
