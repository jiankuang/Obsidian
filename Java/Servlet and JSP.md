# Java Servlet & Jsp
Learning notes about Java Servlet and JSP

## Dynamic Web Project
* Java Resources: place Servlets
* WebContent: place JSP, HTML

# Servlet
## Methods
### doGet
```
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException e {
    PrintWriter print = response.getWriter();
    print.println("<h1>Hello World</h1>");
}
```
## Life Cycle
![Alt text](/img/servlet_life_cycle.PNG?raw=true "Servlet Life Cycle")

# JSP
Implicitly converted into Servlet

## JSP Scripting Element
![Alt text](/img/jsp_scripting_element.PNG?raw=true "JSP Scripting Element")

### Expression
only one single statement  
`<%= out.println("Hello World") %>`  
`<%= new String("Jian") %>` or `<%= "Jian" %>`  
`<%= new java.util.Date() %>`  
`<%= 25 * 10 %>`  
`<%= 25 > 50 %>`  

### Scriptlet
`<% out.println("Hello World"); %>`  
`<% if(25>50) { out.println("True"); } else { out.println("False"); } %>`  
```
<%
int age = 12;
out.println("My age is: " + age);
%>
```

### Declaration
```
<%! public int x=5; %>
<%= x %>
```
```
<%! 
String message() {
    return "Hello World";
}
%>
<%= message() %>
```
### Directive
A JSP directive privides additional information about the page to JSP Engine at page traslation time. This addtional information is used by JSP container and it controls the processing of the entire page accordingly. 

#### Page Directive
The page directive can apply different attributes to JSP page.  
Following are the various page directives that are used in JSP:
* language: `<%@ page language="java" %>`
* extends: `<%@ page extends="com.Connect" %>`
* import: `<%@ page import="java.util.*,java.io.*" %>`
* session: `<%@ page session="true" %>`
* buffer: `<%@ page buffer="8" %>`
* autoFlush
* isThreadSafe
* errorPage
* info
* isErrorPage
* contentType

#### Taglib Directive
It is used to use the custom tags developed by you in JSP & also used to use JSTL tags inside the JSP.  
Syntax: `<%@ taglib uri="some uri" prefix="some prefix" %>`  

#### include Directive
It is used to include one JSP or HTML to another JSP.  
Example: `<%@ include file="/header.jsp" %>`

### Comment
`<%-- response.sendRedirect("http://www.google.com"); --%>`

## JSP Implicit Objects
**Implicit objects** are created by the web container that are available to all the jsp pages. There are in total 9 implicit objects. 

implicit objects | Class
-----------------|-------------------------------------
out              | javax.servlet.jsp.JspWriter
request          | javax.servlet.http.HttpServletRequest
response         | javax.servlet.http.HttpServletResponse
session          | javax.servlet.http.HttpSession
application      | javax.servlet.ServletContext
exception        | javax.servlet.jsp.JspException
Page             | java.lang.Object
pageContext      | javax.servlet.jsp.PageContext
Config           | javax.servlet.ServletConfig

# Citation
JSP and servlet basics, Udemy, https://www.udemy.com/jsp-servlet-free-course/learn/v4/overview
