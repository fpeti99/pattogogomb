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
        int novekmeny_x;
        int novekmeny_y;
        uint ido = 0;
        uint szamlalo = 0;
        Button[] gombok = new Button[100];

        public Form1()
        {
            InitializeComponent();
        }

        void gombok_lerakasa(int hany_gomb)
        {
            int sor = 0;
            int gomb_a_sorban = 0;

            for(int i = 0; i < hany_gomb; i++)
            {
                gombok[i] = new Button();
                if(gombok[i].Width * gomb_a_sorban > Width)
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
                Controls.Add(gombok[i]);
            }
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

            button1.Left = button1.Left + novekmeny_x;
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
            }

            if (button1.Top + button1.Height > button2.Top && button1.Left > button2.Left && button1.Left < button2.Left + button2.Width)
            {
                novekmeny_y = -sebesseg;
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
            button1.Left = 197;
            button1.Top = 98;
            button3.Visible = false;
            button2.Visible = true;
            button1.Visible = true;
            timer1.Enabled = true;
            ido = 0;
            gombok_lerakasa(20);
            /*gomb = new Button();
            gomb.Text = "elso";
            gomb.BackColor = Color.LightBlue;
            Controls.Add(gomb);*/
        }

      
    }
}
