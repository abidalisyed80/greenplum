# Installing Greenplum Database on Ubuntu 18.04 LTS

Follow these steps to install and configure Greenplum Database on Ubuntu 18.04 LTS.

1. **Add hostname entry to `/etc/hosts`**

    ```bash
    sudo vi /etc/hosts
    # Add the following line under '127.0.0.1'
    127.0.0.1 gplum
    ```

2. **Set hostname**

    ```bash
    sudo systemctl set-hostname gplum
    ```

3. **Add Greenplum repository and update**

    ```bash
    sudo apt update
    sudo apt install software-properties-common
    sudo apt update
    ```
    
4. **Install Greenplum Database**
     *Dowload Greenplum part files and extract into a single .deb file ```greenplum-db-6.26.4-ubuntu18.04-amd64.deb```*
    ```bash
      sudo apt install ./greenplum-db-6.26.4-ubuntu18.04-amd64.deb
    ```

6. **Load Greenplum Database software into your environment**

    ```bash
    source /opt/greenplum-db-6.26.4/greenplum_path.sh
    ```
    #installation path may vary , please use your installation path instead of '/opt/'

7. **Edit `gpinitsystem_singlenode` Configuration File**

    ```bash
    cp $GPHOME/docs/cli_help/gpconfigs/gpinitsystem_singlenode .
    # Edit the configuration file as per your requirements
    ```

8. **Add DB server hostname to `/opt/hostlist_singlenode` Configuration File**

    ```bash
    sudo echo “gplum” > /opt/hostlist_singlenode 
    ```

9. **Add Environment values to `.bashrc`**

    ```bash
    cd ~/
    echo  “source /opt/greenplum-db-6.26.4/greenplum_path.sh” >> ~/.bashrc
    echo  “export  MASTER_DATA_DIRECTORY=/opt/gpmaster/gpsne-1” >> ~/.bashrc
    ```

10. **Postgres Configuration**

    Edit `/opt/gpmaster/gpsne-1/pg_hba.conf` and append these lines... REPLACE <USER> with your <SYSTEM_USER> and IP <10.50.50.XX> with trusted IP or IP range to allow access:

    ```bash
    host all all 0.0.0.0/0 md5
    host all all 10.64.50.0/24 md5
    host all all  127.0.0.1/32 trust
    host all <USER> <10.50.50.XX>/32 trust
    host replication <USER> <10.50.50.XX>/32 trust
    host replication <USER> 127.0.0.1/32 trust
    ```

11. **Initialize Greenplum DB server with `gpinitsystem`**

    ```bash
    gpssh-exkeys -h localhost
    gpinitsystem -c gpinitsystem_singlenode
    ```

12. **Start/Stop Database Service**

    ```bash
    # Stop service
    gpstop -i
    # Start service
    gpstart -a
    ```

13. **Create Database User and Database**

    ```bash
    # Create DB user.
    createuser -d -l -W -E -P <user_name>  
    # Create DB 
    createdb <db_name>
    # Grant access to DB
    psql postgres;
    GRANT ALL PRIVILEGES ON DATABASE <db_name> TO <db_user>;
    ```

14. **Test Connection**

    ```bash
    psql -U <db_user> -d <db_name> -h localhost 
    ```

Feel free to modify the steps or add more details as needed.
