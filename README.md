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

        public Form1()
        {
            InitializeComponent();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            button1.Left = button1.Left + novekmeny_x;
            button1.Top = button1.Top + novekmeny_y;
            if (button1.Left + button1.Width + 15 > Width) novekmeny_x = -sebesseg;
            if (button1.Left < 0) novekmeny_x = sebesseg;
            if (button1.Top < 0) novekmeny_y = sebesseg;

            if (button1.Top + button1.Height + 36 > Height)
            {
                timer1.Enabled = false;
                MessageBox.Show("A játéknak vége!");
                Close();
            }

            if (button1.Top + button1.Height > button2.Top && button1.Left > button2.Left && button1.Left < button2.Left + button2.Width)
            {
                novekmeny_y = -sebesseg;
            }

        }

       

             


        

        private void Form1_Load(object sender, EventArgs e)
        {
            timer1.Enabled = true;
            novekmeny_x = sebesseg;
            novekmeny_y = sebesseg;
        }

        private void Form1_MouseMove(object sender, MouseEventArgs e)
        {
            button2.Left = e.X - (button2.Width/2);
        }
    }
}
