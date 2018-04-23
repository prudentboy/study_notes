# lua学习笔记 #

### conf文件 ###
- upstream *server_name* {...}
- server {...}
  - common config:
     - listen      *port*;
     - server_name *domain*;
     - large_client_header_buffers/client_max_body_size/client_body_buffer_size
     - *log_name* *log_path*
  - subdirectory config:
     - location /*subdir* {...}
         - charset *charset*
         - content_by_lua_file *file*
		 - set $*var_name* *var_value
		 - root html;
		 - index index.html index.htm
		 - proxy_http_version *version*
		 - proxy_set_header Connection ""
		 - proxy_pass "*url_path*" (可以使用upstream中定义的内容)
		 - proxy_connect_timeout/proxy_read_timeout/proxy_send_timeout/proxy_buffer_size/proxy_buffers/proxy_busy_buffers_size/proxy_temp_file_write_size/proxy_temp_file_write_size

### lua文件 ###
- 语法
  - 函数
	 - function *func_name*(*para_list...*) ... end
     - 


