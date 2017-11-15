using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using System.Drawing;

namespace button_pingpong
{
    class tegla
    {
        public tegla (int teglak_szama)
        {

        }

        public void gombok_lerakasa(int hany_gomb, Button[] gombok, Form1 form1, int szelesseg)
        {
            int sor = 0;
            int gomb_a_sorban = 0;

            for (int i = 0; i < hany_gomb; i++)
            {
                gombok[i] = new Button();
                if (gombok[i].Width * gomb_a_sorban > szelesseg)
                {
                    sor++;
                    gomb_a_sorban = 0;
                }
                gombok[i].Left = gombok[i].Width * gomb_a_sorban;
                gomb_a_sorban++;
                gombok[i].Top = gombok[i].Height * sor;
                gombok[i].BackColor = Color.DarkRed;
                gombok[i].Text = i.ToString();
                gombok[i].FlatStyle = FlatStyle.Flat;
                form1.Controls.Add(gombok[i]);
            }
        }
    }
}





















using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace button_pingpong
{
    public partial class Form1 : Form
    {
        int sebesseg = 4;
        double novekmeny_x;
        int novekmeny_y;
        uint ido = 0;
        uint szamlalo = 0;
        Button[] gombok = new Button[100];

        int pont = 0;

        public Form1()
        {
            InitializeComponent();
        }

        

        private void timer1_Tick(object sender, EventArgs e)
        {
            szamlalo++;
            if(szamlalo % 100 == 0)
            {
                ido++;
                string szoveg = "Eltelt idő: " + ido.ToString() + " mp.";
                Text = szoveg;
             }

            button1.Left = button1.Left + (int)novekmeny_x;
            button1.Top = button1.Top + novekmeny_y;
            if (button1.Left + button1.Width + 15 > Width) novekmeny_x = -sebesseg;
            if (button1.Left < 0) novekmeny_x = sebesseg;
            if (button1.Top < 0) novekmeny_y = sebesseg;

            if (button1.Top + button1.Height + 36 > Height)
            {
                timer1.Enabled = false;
                button3.Visible = true;
                button2.Visible = false;
                button1.Visible = false;
                button3.Text = "Játék újraindítása!";
                MessageBox.Show(pont + " pontod lett!");
            }

            if (button1.Top + button1.Height > button2.Top && button1.Left > button2.Left && button1.Left < button2.Left + button2.Width)
            {
                novekmeny_y = -sebesseg;
            }

            for(int i = 0; i < 20; i++)
            {
                if(button1.Top < (gombok[i].Top + gombok[i].Height) && button1.Left > gombok[i].Left && button1.Left < (gombok[i].Left + gombok[i].Width))
                {
                    gombok[i].Left = -2000;
                    gombok[i].Top = -2000;
                    novekmeny_x = sebesseg;
                    novekmeny_y = sebesseg;
                    pont++;
                }
            }

            

            if(pont == 20)
            {
                timer1.Enabled = false;
                MessageBox.Show("Nyertél!");
                button3.Visible = true;
            }
       

        }


        private void Form1_Load(object sender, EventArgs e)
        {
            novekmeny_x = sebesseg;
            novekmeny_y = sebesseg;
            button2.Visible = false;
            button1.Visible = false;

        }

        private void Form1_MouseMove(object sender, MouseEventArgs e)
        {
            button2.Left = e.X - button2.Width/2;
        }

        private void button3_Click(object sender, EventArgs e)
        {
            for(int i = 0; i < 20; i++)
            {
                Controls.Remove(gombok[i]);
            }
            button1.Left = 197;
            button1.Top = 98;
            button3.Visible = false;
            button2.Visible = true;
            button1.Visible = true;
            timer1.Enabled = true;
            ido = 0;

            tegla d = new tegla(20);
            d.gombok_lerakasa(20, gombok, this, Width);

            pont = 0;
            /*gomb = new Button();
            gomb.Text = "elso";
            gomb.BackColor = Color.LightBlue;
            Controls.Add(gomb);*/
        }

      
    }
}
