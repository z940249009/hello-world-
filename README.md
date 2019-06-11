package bank_view;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.*;

import bank_dao.cunkuan;
import bank_dao.find;
public class SM extends JFrame{
	public String str1 = null, str2=null, str3=null;
	double l = 0;
      public SM() {
    	  this.setTitle("欢迎进入存款界面");	
    	  this.setSize(380, 500);
    	  this.setLocation(500, 100);
    	  BorderLayout bl=new BorderLayout(10,50);
    	     this.setLayout(bl);

    	  JPanel center =new JPanel(new GridLayout(9, 2, 0, 20));
    	  //this.setContentPane(center);
    	  center.add(new JLabel("账户"));
    	  JTextField text_1 = new JTextField(10);
    	  center.add(text_1);
    	  center.add(new JLabel("密码"));
    	  JPasswordField text_11 = new JPasswordField(10);
    	  center.add(text_11);
    	  center.add(new JLabel("存入金额"));
    	  JTextField text_2 = new JTextField(10);
    	  center.add(text_2);
    	  JButton b1 = new JButton("确认");
    	  b1.addActionListener(new ActionListener(){  
              //单击按钮执行的方法  
              public void actionPerformed(ActionEvent e) {
            	  if(!text_1.getText().trim().equals(""))
            	  {
            		  str1 = text_1.getText();//获取账户
            	  }
            	  
            	  if(!text_2.getText().trim().equals(""))
            	  {
                	  str2 = text_2.getText();//获取取款金额
            	  }
            	  if(!text_11.getText().trim().equals(""))
                  {
            		  str3 = text_11.getText();
                  }
           
                  double money = 0;
                  if(str2!=null&& IO.ok(str2)!=-1) {
                	  money = Double.parseDouble(str2);
                  }
                  
                  try {
                	  if(str1!=null) {
                		  if(cunkuan.add(money,str1)==1) {
      						if(str3!=null) {
      							if(find.findkey(str1, str3)==1)
      						    {
      								if(str2!=null)
      								{
      								  
				            		     if(IO.ok(str2)!=-1)
				            		      {
				            		    	 new back_SM(str1, str2, str3);
				            		      }else {
				            		    	  JOptionPane.showMessageDialog(null, "金额输入不合法", "错误 ",JOptionPane.ERROR_MESSAGE);
				            		      }
				            		  
      							   }
      							   else {
      									JOptionPane.showMessageDialog(null, "金额不能为空", "警告 ",JOptionPane.WARNING_MESSAGE);
      								}
      								
      						 }else {
      							 JOptionPane.showMessageDialog(null, "密码不正确", "错误 ",JOptionPane.ERROR_MESSAGE);
      						 }
      							 
      						 }else {
      							JOptionPane.showMessageDialog(null, "请输入密码", "警告 ",JOptionPane.WARNING_MESSAGE);
      						 }
      						}else {
      							JOptionPane.showMessageDialog(null, "账户不存在", "警告 ",JOptionPane.WARNING_MESSAGE);
      						}	
  							
                	  }else {
                		  JOptionPane.showMessageDialog(null, "请输入账户", "警告 ",JOptionPane.WARNING_MESSAGE);
                	  }
					
				} catch (Exception e2) {
					// TODO Auto-generated catch block
					e2.printStackTrace();
				}
            	  
              }  
                
          });  
    	  
    	  JButton b2 = new JButton("完成");
    	  b2.addActionListener(new ActionListener(){  
              //单击按钮执行的方法  
              public void actionPerformed(ActionEvent e) {  
                  
                  setVisible(false);
                  //new Main_View(); 
                  
              }  
                
          });  
    	  
    	  
    	  
    	  
    	  center.add(b1);
    	  center.add(b2);
    	  this.add(center,"Center");
    	  
    	 /* Icon bg = new ImageIcon("image3.jpg");
  		// 把背景图片显示在一个标签里
  		JLabel label = new JLabel(bg);
  		//把标签的大小位置设置为图片刚好填充整个面
  		label.setBounds(0,0,bg.getIconWidth(),bg.getIconHeight());
  		//添加图片到frame的第二层
  		this.getLayeredPane().add(label,new Integer(Integer.MIN_VALUE));
  		//获取frame的最上层面板为了设置其背景颜色（JPanel有设置透明的方法）
  		JPanel jp=(JPanel)this.getContentPane();
  		jp.setOpaque(false);//设置透明*/
  		center.setOpaque(false);
  		this.setVisible(true);
  		//this.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
      }
      public static void main(String[] args)
  	{
  		new SM();
  		
  	}
}
