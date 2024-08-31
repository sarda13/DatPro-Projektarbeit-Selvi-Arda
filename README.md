VERSION 1

import pygame
import multiprocessing as mp
import queue
import math 
import time
import numpy as np
from mpi4py import MPI


GET_BOX
request: ('GET_BOX', id)
reply: ('GET_BOX', box)

GET_SIZE
request: ('GET_SIZE', id)
reply: ('GET_SIZE', n_workers)

GET_PUCK
request: ('GET_PUCK', n, id)
reply: ('GET_PUCK', puck)

SET_NAME
request: ('SET_NAME', name, secret, id)
reply: ('SET_NAME', name)

SET_ACCELERATION
request: ('SET_ACCELERATION', a, secret, id)
reply: ('SET_ACCELERATION', a)





V_MIN =  10.0
V_MAX =  42.0
A_MAX = 100.0

class Box:

    def __str__(self):
        return f"Box(xmin={self.xmin}, xmax={self.xmax}, "\
                   f"ymin={self.ymin}, ymax={self.ymax})"

    def get_x_limits(self):
        return (self.xmin, self.xmax)

    def get_y_limits(self):
        return (self.ymin, self.ymax)

class Puck:

    RADIUS = 1.0

    def __str__(self):
        return f"Puck(Id={self.id}, Alive={self.alive}, "\
               f"s={self.s}, v={self.v}, a={self.a}"

    def is_alive(self):
        return self.alive

    def get_id(self):
        return self.id

    def get_time(self):
        return self.t

    def get_position(self):
        return self.s

    def get_velocity(self):
        return self.v

    def get_acceleration(self):
        return self.a

    def get_name(self):
        return self.name

    def get_fuel(self):
        return self.fuel

    def get_points(self):
        return self.points
        
def worker_arda(id, secret, q_request, q_reply):
    q_request.put(('SET_NAME', 'Arda', secret, id))
    reply_x = q_reply.get()
    q_request.put(('GET_SIZE', id))
    reply_y = q_reply.get()
    N = reply_y[1]
    for i in range(0, N):





