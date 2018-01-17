title: A simple example in jbpm
date: 2015-06-09 10:43:24
tags:
  - Java
categories:
  - Workflow
---
In some sense, JBPM is simple, because its goal is to offer process management features in a way that both business users and developers like it. Here I will give you a very simple JBPM example with Java action codeblock.
<!--more-->

### JPDL
There is a JBoss jBPM Process Definition Language file, which defines the topology of the application process.

![test1.jpdl.xml](http://7xjjbh.com1.z0.glb.clouddn.com/blog1.jpg)

Suppose one guy("Tom") wants to apply for something, he has to submit his application online at the "Apply" task. Then the application form will moves to a certain assignee(Here I name it is "manager"). If the manager says "Yes", the process moves to the end, and the application successfully ends. If the manager says "No", the process moves back the "Apply" step, and Tom should apply again (Poor Tom~~).

Well, that's the whole process. Simple?

Next, I will show the xml code of the JPDL file.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<process key="test" name="test1" xmlns="http://jbpm.org/4.4/jpdl">
```


### Java Code
Here is the java code that driving the actions of the whole process above. The given code is pretty straightforward. However, the JPDL is more complicated in industry. So you may have more concerns.

```java
package com.tgb.video;

public class JbpmProcess {
	protected RepositoryService repositoryService;
	protected ExecutionService executionService;
	protected TaskService taskService;
	protected String processInstanceID;
	public void deploy() {

	public void createInstance() {
	public String getCurrentInstanceID(){
	public ProcessInstance getProcessInstanceByTaskId(String taskId) {
	public List<ProcessInstance> getProcesInstanceList() {
	public String getProcessDefinitionForm(String taskId) {
	public String  getCurrentActivityName(String processID) {
	public void getTask(String assignee) {
	public void addTaskVariable(String TaskID, String TaskUserID, String TaskUserName){
	public String getTaskVariableID(String TaskID) {
	public String getTaskVariableName(String TaskID) {
	public void completeTask(String TaskID) {
	public void getProcessInstanceVariable(String ProcessID){
	public void updateVariable(String ProcessID, String UserID, String UserName){
	//If Yes, the processInstance moves to the end. If the manager replies "No",  the processInstance goes back to application step  
		else{
	 * */
}
```

### Test
After finishing these steps, you can use JUnit to test your action class. But before that, you need to re-configure the jbpm.hibernate.cfg.xml(import into eclipse).

```
<?xml version="1.0" encoding="utf-8"?>
     <property name="hibernate.dialect">org.hibernate.dialect.MySQLInnoDBDialect</property>
     <mapping resource="jbpm.repository.hbm.xml" />
  </session-factory>

```

Here, I choose MySQL as the jbpm database, and name & username & password you can set as you wish.

### Tips:

1. The first time you deploy the jbpm in your db, there is no table. Therefore, in jbpm.hibernate.cfg.xml, use "create" rather than "update" in the first time. Then you can change back to "update".

2. If the error is about the sql dialect, change "org.hibernate.dialect.MySQLInnoDBDialect" into "org.hibernate.dialect.MySQLDialect".

3. Don't forge to keep your database server on.