sua log batch create_mode=0
->
output SQL


# code for test: create data for advertisers in mariaDB
//        String insertAdvertisersQuery0 = "Insert INTO  advertisers " +
//                "         (name, generate_model, created_at, updated_at, default_advertiser_name, default_advertiser_domain)" +
//                " VALUES ('manh', 1, "+ checkUpdatedDay +", " + checkUpdatedDay + ", 'default_advertiser_name', 'default_advertiser_domain')";
//        MariaDBOperator.execUpdateOnNewConn(env.toString().toLowerCase(), insertAdvertisersQuery0);


        String updateAdvertisersQuery0 = "UPDATE advertisers SET updated_at = '20190101', generate_model = '1' WHERE id IN (2, 3)";
        MariaDBOperator.execUpdateOnNewConn(env.toString().toLowerCase(), updateAdvertisersQuery0);

        String selectAdvertisersQuery0 = "SELECT * from advertisers order by id";
        ResultSet rs = MariaDBOperator.execQueryOnNewConn(env.toString().toLowerCase(), selectAdvertisersQuery0);
        while ((rs.next())) {
            Integer id = rs.getInt("id");
            Integer generate_model = rs.getInt("generate_model");
            String updated_at = rs.getString("updated_at");
            System.out.println("id: " + id + ", generate_model: " + generate_model + ", updated_at: " + updated_at);
        }

# migration
bin/rails generate migration AddPartNumberToProducts


# INSERT data into log table
INSERT INTO
  `${BATCH_DATA_SET}.reset_create_model_advertisers_${TODAY}` (id)
VALUES
  ${ADVERTISER_ID_LIST}

# CREATE TABLE AND INSERT data in one SQL
CREATE TABLE IF NOT EXISTS
  `tmp.reset_create_model_advertisers_20190608`( id int64 )
AS   select id from (
    select 1 as id  union all
    select 3 as id  union all
    select 5 as id  union all
    select 7 as id
  )
