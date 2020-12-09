# lab4
## 实验目的
掌握字符串String及其方法的使用
掌握文件的读取/写入方法
掌握异常处理结构
## 阅读程序
package vv;

import java.util.Scanner;

public class Student {
	String name;
	String sex;
	int age;
	String stuNo;

public void inputInformation() {
	Scanner reader = new Scanner(System.in);
	a:for(;;) {
		try {
			System.out.println("请输入姓名");
	        name=reader.nextLine();
	        System.out.println("录入成功~");
	        break a;
		}
		catch(Exception e) {
			System.out.println("您输入的 “"+name+"” 格式不正确，请重新输入！");
		}
	}
	b:for(;;) {
	try{
	System.out.println("请输入性别（中文）");
	sex=reader.nextLine();
	sexJudge(sex);
	break b;
	}
	catch(JudgeException e) {
		System.out.println(e.JudgeException(sex));
	}
	}
	c:for(;;) {
		try{
			System.out.println("请输入年龄（15-75岁）");
			age=reader.nextInt();
		    ageJudge(age);
		    break c;
		}
		catch(JudgeException e) {
			System.out.println(e.JudgeException(age));
		}
		}
	d:for(;;) {
		try {
			Scanner reader0 = new Scanner(System.in);
			System.out.println("请输入学号");
			stuNo=reader0.nextLine();
	        System.out.println("录入成功~");
	        break d;
		}
		catch(Exception e) {
			System.out.println("您输入的“"+stuNo+"”格式不正确，请重新输入！");
		}
	}
	
}
public void sexJudge(String sex) throws JudgeException{
	String x="男";
	String y="女";
	if (sex.equals(x)||sex.equals(y)){
		System.out.println("录入成功~");
		}
	else throw new JudgeException();
}
public void ageJudge(int age) throws JudgeException{
	int x=15;
	int y=75;
	if (age>=x&&age<=y){
		System.out.println("录入成功~");
		}
	else throw new JudgeException();
}

}


package vv;

public class Test {
	static Student student0=new Student();
	static FileInAndOut file = new FileInAndOut();
	public static void main(String[] args) {
		
		  System.out.println("第四次实验：文件操作");
		  System.out.println("**********学生信息录入**********");//10
		  student0.inputInformation(); 
		  System.out.println("\n\n个人信息：");
		  System.out.println("姓名 性别 年龄       学号    ");
		  System.out.println(student0.name+"   "+student0.sex+"    "+student0.age+"    "+student0.stuNo);
		
		String a=file.readFile();
		String b = file.operationFile(a);
		if(file.outFile(addNewInformation(student0)))
		System.out.println("信息导入成功！");
		if(file.outFile(b))
			System.out.println("作业导入成功！");

	}
	public static String addNewInformation(Student student) {
		String information = null;
		information="个人信息：\n姓名 性别 年龄       学号    \n"+student0.name+"   "+student0.sex+"    "+student0.age+"    "+student0.stuNo+"\n完成作业：\n";
		 return information;
	}
}


package vv;

public class JudgeException extends Exception{
	
	String message;
	public String JudgeException(String input) {
		message = "您输入的“"+input+"”不正确，请输入正确性别！";
		return message;
	}
	
	public String JudgeException(int input) {
		message = "您输入的“"+input+"”不正确，请输入正确年龄！";
		return message;
	}
}



package vv;

import java.io.*;
import java.util.Scanner;

public class FileInAndOut {
	int n;
	public String operationFile(String longer) {
		StringBuffer l=new StringBuffer(longer);

		String s;
	    char[] a;
		for(int i = 0;i<l.length();i=i+7) {
			 a=new char[7];
			 try {
				 longer.getChars(i, i+7, a, 0);
		       } catch( Exception ex) {
		            System.out.println("´¥·¢Òì³£...");
		        }
			s = String.valueOf(a);
			StringBuffer t = new StringBuffer(s);
			if(l!=null)
				l=l.append(t);
			if(((i+7)/7)%2==1) {
				l=l.append(",");
				}
			else if(((i+7)/7)%2==0) {
				l=l.append("¡£\n");
			}
			
		}
		String b=l.toString();
		return b;
	}
	
	public String readFile() {
		String original = null;
		int n=-1;
		char[] a = new char[100];//»º´æ£¬
		try {
			File file = new File("e:\\B.txt");
			InputStream fli = new FileInputStream(file);
			InputStreamReader in = new InputStreamReader(fli, "GBK");
		while((n=in.read(a,0,100))!=-1) {
		String s = new String(a,0,n);
		this.n=n;
		if(original!=null)
		original = original+s;
		else original=s;
		}
		
        in.close();
      	}
		catch (IOException e) {
			System.out.println("File read erroe:"+e);
		}
		return original;
	}
	public boolean outFile(String a) {
		byte [] b = a.getBytes();
		try {
			File file = new File("e:\\A.txt");
			OutputStream out = new FileOutputStream(file,true);
			
            out.write(b);
            out.flush();
            out.close();
           
		}
		catch (IOException e) {
			System.out.println("File read erroe:"+e);
		}
		 return true;
		}
	
}

## 心得体会
经过实验掌握了java程序的特征与功能，java中的各种访问控制关键字的作用范围及它们的使用。由于时间仓促，还有许多其他的实验没有亲手
去做，并做做的实验中也有不足的地方，还需要进一步对其进行修。在过程中不断加深对java程序设计的认识和理解，丰富自己的知识，加强自
己的理解能力和学习能力，提高自己独立解决问题的能力。Java是一门全新的计算机语言，需要自己对其全新的理解，而java的很多功能都需要
在学习中去发现和理解，应用到不同的设计中去，并结合网络这个以有利工具方便自己学习java的语言和强大的编码能力，以及在以后的设计中把
程序不断完善。
