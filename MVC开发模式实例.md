# MVC开发模式实例 #

>View层

````html
<html>
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>用户管理</title>
<link rel="stylesheet" type="text/css" href="css/style.css" />
<link rel="stylesheet" type="text/css" href="css/waves.min.css"  />
<link rel="stylesheet" type="text/css" href="css/bootstrap.min.css" />
<script language="javascript" type="text/javascript" src="js/js.js"></script>
<script language="javascript" type="text/javascript" src="js/jquery-3.2.1.min.js"></script>

<script language="javascript" src="js/bootstrap.min.js"></script>

</head>

<body>
<div id="d1">
	<div id="d1_0" style="display:none;width:46px;height:46px;" onclick="d100(),d10()" class="xwcms"></div>
	<div id="d1_1" style="display:block;">权限管理系统</div>
    <div id="d1_2">
      <div class="dropdown">
        <div class="b1 waves-effect waves-light" data-toggle="dropdown" ></div>
        <div class="b12 dropdown-menu dropdown-menu-right"></div>
      </div>
      <div class="dropdown">
      	<div class="b2 waves-effect waves-light" data-toggle="dropdown"></div>
        <div class="b22 dropdown-menu dropdown-menu-right""></div>
      </div>
      <div class="dropdown">
      	<div class="b3 waves-effect waves-light" data-toggle="dropdown"></div>
      	<div class="b32 dropdown-menu dropdown-menu-right""></div>
      </div>
    </div>
</div>

<div id="d2">
	<div id="d2_left" style="display:block">
    	<div id="lef1" class="waves-effect waves-light" onclick="ff(),a()">
        	<div class="xwcms" id="i1"></div>
        </div>
        <div id="y1">
        	<div id="l1" class="waves-effect"><div>个人资料</div></div>
            <div id="l2" class="waves-effect"><div>隐私管理</div></div>
            <div id="l3" class="waves-effect"><div>系统设置</div></div>
            <div id="l4" class="waves-effect"><div>退出登录</div></div>
        </div>

        <div id="caidan">
    		<div id="c1" class="waves-effect" onclick="ffshou(),ifr1()"><div>首页</div></div>

        	<div id="c2" class="waves-effect" onclick="b(),c22()">
            	<div id="c21">系统组织管理</div>
                <div id="c22" class="xwcms"></div>
            </div>
            <div id="c2y">
            	<div id="c2y1" class="waves-effect" onclick="ffxi(),ifr2()">系统管理</div>
                <div id="c2y2" class="waves-effect" onclick="ffzu(),ifr3()">组织管理</div>
            </div>

        	<div id="c3" class="waves-effect" onclick="c3y(),c32()">
            	<div id="c31">角色用户管理</div>
                <div id="c32" class="xwcms"></div>
            </div>
            <div id="c3y">
            	<div id="c3y1" class="waves-effect" onclick="ffjue()">角色管理</div>
                <div id="c3y2" class="waves-effect" onclick="ffyong(),ifr5()">用户管理</div>
            </div>

        	<div id="c4" class="waves-effect" onclick="c4y(),c42()">
            	<div id="c41">系统权限管理</div>
                <div id="c42" class="xwcms"></div>
            </div>
            <div id="c4y">
            	<div id="c4y1" class="waves-effect" onclick="ffquan()">权限管理</div>
            </div>

        	<div id="c5" class="waves-effect" onclick="c5y(),c52()">
            	<div id="c51">其他数据管理</div>
                <div id="c52" class="xwcms"></div>
            </div>
            <div id="c5y">
            	<div id="c5y1" class="waves-effect" onclick="ffgong()">公共码表</div>
                <div id="c5y2" class="waves-effect" onclick="ffhui()">会话管理</div>
                <div id="c5y3" class="waves-effect" onclick="ffri()">日志记录</div>
                <div id="c5y4" class="waves-effect" onclick="ffjian()">键值设置</div>
            </div>

    	</div>

        <div class="banquan">
        	&copy;ZHENG-UPMS&nbsp;V1.0.0
        </div>

    </div>



	<div id="d2_right">
    	<div id="nav">

        	<div id="n_1" class="waves-effect waves-light" onclick="ifr1()">首页</div>

      </div>
      <div class="dropdown bootstrapMenu" style="z-index: 5;position: absolute; display: none; height:                    100px; width: 100px; top: 150px;">
				<ul class="dropdown-menu" style="position: static;display: block;font-size: 0.8em;">
					<li><a href="#" role="menuitem">关闭</a></li>
					<li><a href="#" role="menuitem">刷新</a></li>
					<li><a href="#" role="menuitem">关闭其他</a></li>
					<li><a href="#" role="menuitem">关闭全部</a></li>
					<li><a href="#" role="menuitem">关闭右侧所有</a></li>
					<li><a href="#" role="menuitem">关闭左侧所有</a></li>
				</ul>
			</div>
        <div id="iframech">
        <iframe src="http://jquery.cuishifeng.cn/" id="ifr1">

        </iframe>
        </div>
    </div>
</div>

</body>
````

>controller层

````java
//Servlet
public class TServlet1 extends HttpServlet {
    UserService userService = new Tservice1();
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        List<User> user = userService.getUser();
        req.setAttribute("user",user);
        this.getServletConfig().getServletContext().getRequestDispatcher("/users/users1.jsp").forward(req,resp);
    }
}

//service
public interface UserService {
    public List<User> getUser();
}

public class Tservice1 implements UserService {
    UserDao userDao = new Tdao1();
    public List<User> getUser(){
        return userDao.getAllusers();
    }
}


//Dao
public interface UserDao {
    public List<User> getAllusers();
}

public class Tdao1 implements UserDao {

    @Override
    public List<User> getAllusers() {
        //连接数据库
        List<User> ulist = new ArrayList<User>();
        Connection con;
        String driver = "com.mysql.jdbc.Driver";
        String url = "jdbc:mysql://localhost:3306/***";
        String user = "***";
        String password = "***";

        try{
            //加载驱动程序
            Class.forName(driver);
            //1.getConnection()方法,连接MySQL数据库
            con = DriverManager.getConnection(url,user,password);
            if(!con.isClosed()){
                System.out.println("Succeeded connecting to the Database!");
            }
            Statement statement = con.createStatement();
            PreparedStatement ps;
            ResultSet rs;
            String sql = "SELECT * FROM xxx";
            ps = con.prepareStatement(sql);
            ResultSet res = ps.executeQuery();

            while(res.next()) {
                int id = res.getInt(1);
                String name = res.getString(2);
                User user1 = new User(id,name);
                ulist.add(user1);
            }

        }catch(Exception e){

        }
        return ulist;
    }
}
````

>Model层

````java
public class User {
    private int id;
    private String name;
    public User(int id,String name){
        this.id=id;
        this.name=name;
    }

    public void setId(int id) {
        this.id = id;
    }
    public void setName(String name){
        this.name=name;
    }

    public int getId() {
        return id;
    }
    public String getName(){
        return name;
    }
}
````
