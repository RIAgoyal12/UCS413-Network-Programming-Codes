#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <netinet/in.h>
#include <string.h>

#define  err_log(log) do{perror(log); exit(1);}while(0)
#define  N  128

int main(int argc, const char *argv[])
{

    int sockfd;
    char buf[N];
    struct sockaddr_in broadcastaddr, srcaddr;

    if((sockfd = socket(AF_INET, SOCK_DGRAM, 0)) < 0)
    {
        err_log("fail to socket");
    }

    broadcastaddr.sin_family = AF_INET;
    broadcastaddr.sin_addr.s_addr = INADDR_ANY;   
    broadcastaddr.sin_port = htons(10000);

    if(bind(sockfd, (struct sockaddr*)&broadcastaddr, sizeof(broadcastaddr)) < 0)
    {
        err_log("fail to bind");
    }

    socklen_t addrlen = sizeof(struct sockaddr);

    while(1)
    {
        if(recvfrom(sockfd,buf, N, 0, (struct sockaddr *)&srcaddr, &addrlen) < 0)
        {
            err_log("fail to sendto");
        }
        printf("buf:%s ---> %s %d\n", buf, inet_ntoa(srcaddr.sin_addr), ntohs(srcaddr.sin_port));
        
    }
    
    return 0;
}
