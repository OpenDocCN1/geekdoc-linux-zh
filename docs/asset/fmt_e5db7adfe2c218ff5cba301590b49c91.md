
```sql
CREATE INDEX idx_users_username ON users(username);
```

在 `tasks` 表的 `project_id` 列上创建索引，以便通过项目更快访问任务：

```sql
CREATE INDEX idx_tasks_project_id ON tasks(project_id);
```

## 示例：为 AlphaProject 创建数据库架构

现在我们已经有了计划，将开始构建 AlphaProject 的数据库架构。确保你已以 PostgreSQL 用户身份登录并连接到 `alphaproject_db` 数据库：

```bash
$ sudo -i -u postgres
$ psql
```

如果数据库尚未创建，请创建它：

```sql
CREATE DATABASE alphaproject_db;
\c alphaproject_db
```

执行 SQL 命令创建 `users` 和 `time_entries` 表。

然后，创建用户表（Users Table）：

```sql
CREATE TABLE users (
id SERIAL PRIMARY KEY,
username VARCHAR(50) UNIQUE NOT NULL,
password VARCHAR(255) NOT NULL,
email VARCHAR(100) UNIQUE NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

创建项目表（Projects Table）：

```sql
CREATE TABLE projects (
id SERIAL PRIMARY KEY,
name VARCHAR(100) NOT NULL,
description TEXT,
start_date DATE,
end_date DATE,
created_by INT REFERENCES users(id),
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

创建任务表（Tasks Table）：

```sql
CREATE TABLE tasks (
id SERIAL PRIMARY KEY,
project_id INT REFERENCES projects(id),
name VARCHAR(100) NOT NULL,
description TEXT,
status VARCHAR(20) DEFAULT 'pending',
assigned_to INT REFERENCES users(id),
due_date DATE,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

创建时间记录表（TimeEntries Table）：

```sql
CREATE TABLE time_entries (
id SERIAL PRIMARY KEY,
task_id INT REFERENCES tasks(id),
user_id INT REFERENCES users(id),
hours DECIMAL(5, 2) NOT NULL,
entry_date DATE NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

创建索引以增强性能。

```sql
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_tasks_project_id ON tasks(project_id);
```

通过查询数据库验证表和索引是否已正确创建：

```bash
\d
```

此命令将列出所有表，而 `\d table_name` 将显示特定表的详情。

## 与 AlphaProject 的数据库集成

现在数据库架构已经就绪，你可以将其与 AlphaProject 应用程序集成。确保你的应用程序使用了正确的连接设置，并执行必要的数据库操作，如创建、读取、更新和删除记录。

例如，在运行 SQLAlchemy 的 Python 应用中：

```python
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
DATABASE_URL = "postgresql://alphaproject_user:yourpassword@localhost/alphaproject_db"
engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()
```

定义映射到数据库表的模型：

```python
from sqlalchemy import Column, Integer, String, Text, ForeignKey,
Date, DECIMAL, TIMESTAMP
from sqlalchemy.orm import relationship
class User(__tablename__='users'):
id = Column(Integer, primary_key=True, index=True)
username = Column(String(50), unique=True, nullable=False)
password = Column(String(255), nullable=False)
email = Column(String(100), unique=True, nullable=False)
created_at = Column(TIMESTAMP)
```

```python
class Project(__tablename__='projects'):
id = Column(Integer, primary_key=True)
name = Column(String(100), nullable=False)
description = Column(Text)
start_date = Column(Date)
end_date = Column(Date)
created_by = Column(Integer, REFERENCES(users.id))
created_at = Column(TIMESTAMP)
```

```python
class Task(__tablename__='tasks'):
id = Column(Integer, primary_key=True)
project_id = Column(Integer, REFERENCES(projects.id))
name = Column(String(100), nullable=False)
description = Column(Text)
status = Column(String(20), default='pending')
assigned_to = Column(Integer, REFERENCES(users.id))
due_date = Column(Date)
created_at = Column(TIMESTAMP)
```

```python
class TimeEntry(__tablename__='time_entries'):
id = Column(Integer, primary_key=True)
task_id = Column(Integer, REFERENCES(tasks.id))
user_id = Column(Integer, REFERENCES(users.id))
hours = Column(DECIMAL(5, 2), NOT NULL)
entry_date = Column(Date, NOT NULL)
created_at = Column(TIMESTAMP)
```

创建索引以增强性能。

```sql
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_tasks_project_id ON tasks(project_id);
```

通过查询数据库验证表和索引是否已正确创建：

```bash
\d
```

此命令将列出所有表，而 `\d table_name` 将显示特定表的详情。

## AlphaProject 数据库集成

现在数据库架构已经到位，你可以将其与 AlphaProject 应用程序集成。确保你的应用程序使用正确的连接设置并执行必要的数据库操作（创建、读取、更新和删除）。

例如，在使用 SQLAlchemy 的 Python 应用中：
