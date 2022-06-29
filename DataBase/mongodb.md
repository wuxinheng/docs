| MongoDB | Sql server |
| ------- | ---------- |
| 数据库  | 数据库     |
| 集合    | 表         |

```c#

using MongoDB.Driver;
using System;
using System.Collections.Generic;
using System.Text;


namespace MongoDB.Service
{
   public class DBherper
    {
        #region 连接数据库
        /// <summary>
        /// 获取MongoDB DataBase,如果不存在数据库，将会自动创建
        /// </summary>
        /// <param name="currDBHost">主机地址</param>
        /// <param name="currDBName">数据库名称</param>
        /// <returns>MongoDB数据库对象</returns>
        private static IMongoDatabase GetDatabase(string currDBHost = "mongodb://localhost", string currDBName = "myMongoDB")
        {
            IMongoDatabase mongoDatabase;
            try
            {
                MongoClient mongoClient = new MongoClient(currDBHost);
                mongoDatabase = mongoClient.GetDatabase(currDBName);
            }
            catch (Exception)
            {
                throw;
            }
            return mongoDatabase;
        }
        #endregion

        #region 删除数据库
        /// <summary>
        /// 删除数据库
        /// </summary>
        /// <param name="currDBHost">主机地址</param>
        /// <param name="currDBName">数据库名称</param>
        /// <returns>结果</returns>
        private static bool DropDatabase(string currDBHost = "mongodb://localhost", string currDBName = "myMongoDB")
        {
            bool result = true;
            try
            {
                MongoClient mongoClient = new MongoClient(currDBHost);
                mongoClient.DropDatabase(currDBName);
            }
            catch (Exception)
            {
                result = false;
                throw;
            }
            return result;
        }
        #endregion

        #region 异步删除数据库
        /// <summary>
        /// 异步删除数据库
        /// </summary>
        /// <param name="currDBHost">主机地址</param>
        /// <param name="currDBName">数据库名称</param>
        /// <returns>结果</returns>
        private static bool DropDatabaseAsync(string currDBHost = "mongodb://localhost", string currDBName = "myMongoDB")
        {
            bool result = true;
            try
            {
                MongoClient mongoClient = new MongoClient(currDBHost);
                mongoClient.DropDatabaseAsync(currDBName);
            }
            catch (Exception)
            {
                result = false;
                throw;
            }
            return result;
        }
        #endregion

        #region 插入单个文档
        /// <summary>
        /// 插入单个文档
        /// </summary>
        /// <typeparam name="T">操作对象类型</typeparam>
        /// <param name="model">需要操作的对象Model</param>
        /// <param name="collectionName">集合名称</param>
        public static bool InsertOne<T>(T model, string collectionName)
        {
            bool result = true;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                dbCollection.InsertOne(model);

            }
            catch (Exception)
            {
                result = false;
                throw;
            }
            return result;
        }
        #endregion

        #region 异步插入单个文档
        /// <summary>
        /// 异步插入单个文档
        /// </summary>
        /// <typeparam name="T">操作对象类型</typeparam>
        /// <param name="model">需要操作的对象Model</param>
        /// <param name="collectionName">集合名称</param>
        public static bool InsertOneAsync<T>(T model, string collectionName)
        {
            bool result = true;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                dbCollection.InsertOneAsync(model);

            }
            catch (Exception)
            {
                result = false;
                throw;
            }
            return result;
        }
        #endregion

        #region 插入多个文档
        /// <summary>
        /// 插入多个文档
        /// </summary>
        /// <typeparam name="T">操作对象类型</typeparam>
        /// <param name="model">需要操作的对象Model</param>
        /// <param name="collectionName">集合名称</param>
        public static bool InsertMany<T>(List<T> model, string collectionName)
        {
            bool result = true;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                IEnumerable<T> ts = model;
                dbCollection.InsertMany(ts);
            }
            catch (Exception)
            {
                result = false;
                throw;
            }
            return result;
        }
        #endregion

        #region 异步插入多个文档
        /// <summary>
        /// 异步插入多个文档
        /// </summary>
        /// <typeparam name="T">操作对象类型</typeparam>
        /// <param name="model">需要操作的对象Model</param>
        /// <param name="collectionName">集合名称</param>
        public static bool InsertManyAsync<T>(List<T> model, string collectionName)
        {
            bool result = true;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                IEnumerable<T> ts = model;
                dbCollection.InsertManyAsync(ts);
            }
            catch (Exception)
            {
                result = false;
                throw;
            }
            return result;
        }
        #endregion

        #region 删除单个文档
        /// <summary>
        /// 删除单个文档
        /// </summary>
        /// <typeparam name="T">指定的类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="filterDefinition">条件</param>
        public static bool DeleteOne<T>(string collectionName, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                DeleteResult deleteResult = dbCollection.DeleteOne(filterDefinition);
                if (deleteResult.DeletedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 异步删除单个文档
        /// <summary>
        /// 异步删除单个文档
        /// </summary>
        /// <typeparam name="T">指定的类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="filterDefinition">条件</param>
        public static bool DeleteOneAsync<T>(string collectionName, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                var deleteResult = dbCollection.DeleteOneAsync(filterDefinition).Result;
                if (deleteResult.DeletedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 删除删除多个文档
        /// <summary>
        /// 删除单个文档
        /// </summary>
        /// <typeparam name="T">指定的类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="filterDefinition">条件</param>
        public static bool DeleteMany<T>(string collectionName, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);

                DeleteResult deleteResult = dbCollection.DeleteMany(filterDefinition);
                if (deleteResult.DeletedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 异步删除单个文档
        /// <summary>
        /// 异步删除多个文档
        /// </summary>
        /// <typeparam name="T">指定的类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="filterDefinition">条件</param>
        public static bool DeleteManyAsync<T>(string collectionName, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                DeleteResult deleteResult = dbCollection.DeleteManyAsync(filterDefinition).Result;
                if (deleteResult.DeletedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 更新单个文档
        /// <summary>
        /// 更新单个文档
        /// </summary>
        /// <typeparam name="T">指定的数据类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="updateDefinition">需要修改的信息</param>
        /// <param name="filterDefinition">条件</param>
        public static bool UpdateOne<T>(string collectionName, UpdateDefinition<T> updateDefinition, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                UpdateResult updateResult = dbCollection.UpdateOne(filterDefinition, updateDefinition);
                if (updateResult.ModifiedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 异步更新单个文档
        /// <summary>
        /// 异步更新单个文档
        /// </summary>
        /// <typeparam name="T">指定的数据类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="updateDefinition">需要修改的信息</param>
        /// <param name="filterDefinition">条件</param>
        public static bool UpdateOneAsync<T>(string collectionName, UpdateDefinition<T> updateDefinition, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                //UpdateResult updateResult = dbCollection.UpdateOneAsync(filterDefinition, updateDefinition);
                //if (updateResult.ModifiedCount > 0)
                //{
                //    result = true;
                //}
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 更新多个文档
        /// <summary>
        /// 更新多个文档
        /// </summary>
        /// <typeparam name="T">指定的数据类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="updateDefinition">需要修改的信息</param>
        /// <param name="filterDefinition">条件</param>
        public static bool UpdateMany<T>(string collectionName, UpdateDefinition<T> updateDefinition, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                UpdateResult updateResult = dbCollection.UpdateMany(filterDefinition, updateDefinition);
                if (updateResult.ModifiedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

        #region 异步更新多个文档
        /// <summary>
        /// 异步更新多个文档
        /// </summary>
        /// <typeparam name="T">指定的数据类型</typeparam>
        /// <param name="collectionName">集合名称</param>
        /// <param name="updateDefinition">需要修改的信息</param>
        /// <param name="filterDefinition">条件</param>
        public static bool UpdateManyAsync<T>(string collectionName, UpdateDefinition<T> updateDefinition, FilterDefinition<T> filterDefinition)
        {
            bool result = false;
            try
            {
                var db = GetDatabase();
                var dbCollection = db.GetCollection<T>(collectionName);
                UpdateResult updateResult = dbCollection.UpdateManyAsync(filterDefinition, updateDefinition).Result;
                if (updateResult.ModifiedCount > 0)
                {
                    result = true;
                }
            }
            catch (Exception)
            {

                throw;
            }
            return result;
        }
        #endregion

    }
}

```



```bash
主要命令：
创建数据库
use DB_Name
DB_Name
查看所有数据库
show dbs
插入数据
db.DB_Name.insert({"id":"1"}})
注意：没有插入数据的是数据库show dbs 不会显示
删除数据库
db.dorpDataBase()
创建集合
db.createCollection("集合名称",可选参数)
db.createCollection("mycol", { capped : true, autoIndexId : true, size : 
   6142800, max : 10000 } )
capped:创建固定集合，当指定为true时，必须指定size，当达到最大值时，会自动覆盖最早的文档
autoIndexId:3.2之后不再使用，默认为false,当值为true时，自动再_id字段创建索引。
size:为固定集合指定一个最大值，即最大字节数
max:固定集合中包含文档的最大数量
查看集合
show tables
show conllections
删除集合
db.集合名称.dorp()
```

