#this is the python game script








def draw_court_detailed(self, court: Court):
        """Draw detailed court with all lines and zones"""
        # Draw court base with realistic colors
        court_corners = [
            Vector3D(0, 0, 0),
            Vector3D(court.width, 0, 0), 
            Vector3D(court.width, court.height, 0),
            Vector3D(0, court.height, 0)
        ]
        
        projected_corners = [self.project_3d_to_2d(corner) for corner in court_corners]
        
        # Main court area - realistic green court color
        self.canvas.create_polygon(
            [coord for point in projected_corners for coord in point],
            fill="#2E8B57", outline="white", width=4  # Sea green for indoor court
        )
        
        # Add court texture/pattern
        self.draw_court_texture(court)
        
        # Draw all court lines
        self.draw_badminton_court_lines(court)
        
        # Draw net structure
        self.draw_realistic_net_structure(court)
        
        # Draw court surroundings
        self.draw_court_surroundings()
    
        def draw_court_texture(self, court: Court):
        """Add texture pattern to the court"""
        # Draw subtle grid pattern
        grid_spacing = 30
        
        # Vertical lines
        for i in range(0, int(court.width), grid_spacing):
            start = self.project_3d_to_2d(Vector3D(i, 0, 0))
            end = self.project_3d_to_2d(Vector3D(i, court.height, 0))
            self.canvas.create_line(start[0], start[1], end[0], end[1],
                                  fill="#228B22", width=1, dash=(2, 8))
        
        # Horizontal lines
        for j in range(0, int(court.height), grid_spacing):
            start = self.project_3d_to_2d(Vector3D(0, j, 0))
            end = self.project_3d_to_2d(Vector3D(court.width, j, 0))
            self.canvas.create_line(start[0], start[1], end[0], end[1],
                                  fill="#228B22", width=1, dash=(2, 8))
    
    def draw_badminton_court_lines(self, court: Court):
        """Draw accurate badminton court lines"""
        line_width = 3
        line_color = "white"
        
        # Outer boundary lines (doubles court)
        # Top and bottom lines
        top_line_start = self.project_3d_to_2d(Vector3D(0, 0, 0))
        top_line_end = self.project_3d_to_2d(Vector3D(court.width, 0, 0))
        self.canvas.create_line(top_line_start[0], top_line_start[1], 
                              top_line_end[0], top_line_end[1],
                              fill=line_color, width=line_width)
        
        bottom_line_start = self.project_3d_to_2d(Vector3D(0, court.height, 0))
        bottom_line_end = self.project_3d_to_2d(Vector3D(court.width, court.height, 0))
        self.canvas.create_line(bottom_line_start[0], bottom_line_start[1], 
                              bottom_line_end[0], bottom_line_end[1],
                              fill=line_color, width=line_width)
        
        # Side lines
        left_line_start = self.project_3d_to_2d(Vector3D(0, 0, 0))
        left_line_end = self.project_3d_to_2d(Vector3D(0, court.height, 0))
        self.canvas.create_line(left_line_start[0], left_line_start[1],
                              left_line_end[0], left_line_end[1],
                              fill=line_color, width=line_width)
        
        right_line_start = self.project_3d_to_2d(Vector3D(court.width, 0, 0))
        right_line_end = self.project_3d_to_2d(Vector3D(court.width, court.height, 0))
        self.canvas.create_line(right_line_start[0], right_line_start[1],
                              right_line_end[0], right_line_end[1],
                              fill=line_color, width=line_width)
        
        # Center line (net line)
        center_start = self.project_3d_to_2d(Vector3D(0, court.height // 2, 0))
        center_end = self.project_3d_to_2d(Vector3D(court.width, court.height // 2, 0))
        self.canvas.create_line(center_start[0], center_start[1], 
                              center_end[0], center_end[1],
                              fill=line_color, width=line_width)
        
        # Service lines
        # Short service lines
        short_service_near_y = court.height * 0.3
        short_service_far_y = court.height * 0.7
        
        short_near_start = self.project_3d_to_2d(Vector3D(0, short_service_near_y, 0))
        short_near_end = self.project_3d_to_2d(Vector3D(court.width, short_service_near_y, 0))
        self.canvas.create_line(short_near_start[0], short_near_start[1],
                              short_near_end[0], short_near_end[1],
                              fill=line_color, width=line_width)
        
        short_far_start = self.project_3d_to_2d(Vector3D(0, short_service_far_y, 0))
        short_far_end = self.project_3d_to_2d(Vector3D(court.width, short_service_far_y, 0))
        self.canvas.create_line(short_far_start[0], short_far_start[1],
                              short_far_end[0], short_far_end[1],
                              fill=line_color, width=line_width)
        
        # Singles sidelines (inner lines)
        singles_left_x = court.width * 0.15
        singles_right_x = court.width * 0.85
        
        # Left singles line
        singles_left_start = self.project_3d_to_2d(Vector3D(singles_left_x, 0, 0))
        singles_left_end = self.project_3d_to_2d(Vector3D(singles_left_x, court.height, 0))
        self.canvas.create_line(singles_left_start[0], singles_left_start[1],
                              singles_left_end[0], singles_left_end[1],
                              fill=line_color, width=line_width)
        
        # Right singles line  
        singles_right_start = self.project_3d_to_2d(Vector3D(singles_right_x, 0, 0))
        singles_right_end = self.project_3d_to_2d(Vector3D(singles_right_x, court.height, 0))
        self.canvas.create_line(singles_right_start[0], singles_right_start[1],
                              singles_right_end[0], singles_right_end[1],
                              fill=line_color, width=line_width)
        
        # Center service line (divides left and right service courts)
        center_service_start = self.project_3d_to_2d(Vector3D(court.width // 2, short_service_near_y, 0))
        center_service_end = self.project_3d_to_2d(Vector3D(court.width // 2, short_service_far_y, 0))
        self.canvas.create_line(center_service_start[0], center_service_start[1],
                              center_service_end[0], center_service_end[1],
                              fill=line_color, width=line_width)
    
    def draw_realistic_net_structure(self, court: Court):
        """Draw a realistic badminton net"""
        net_y = court.net_position
        net_height = court.net_height
        net_width = court.width
        
        # Net posts (more realistic)
        post_width = 8
        post_height = net_height + 30
        
        # Left post
        left_post_bottom = self.project_3d_to_2d(Vector3D(-15, net_y, 0))
        left_post_top = self.project_3d_to_2d(Vector3D(-15, net_y, post_height))
        self.draw_net_post(left_post_bottom, left_post_top, post_width)
        
        # Right post
        right_post_bottom = self.project_3d_to_2d(Vector3D(net_width + 15, net_y, 0))
        right_post_top = self.project_3d_to_2d(Vector3D(net_width + 15, net_y, post_height))
        self.draw_net_post(right_post_bottom, right_post_top, post_width)
        
        # Net tape (top white band)
        net_top_start = self.project_3d_to_2d(Vector3D(-10, net_y, net_height))
        net_top_end = self.project_3d_to_2d(Vector3D(net_width + 10, net_y, net_height))
        self.canvas.create_line(net_top_start[0], net_top_start[1],
                              net_top_end[0], net_top_end[1],
                              fill="white", width=6)
        
        # Net mesh - detailed pattern
        self.draw_net_mesh(net_y, net_height, net_width)
        
        # Net bottom cord
        net_bottom_start = self.project_3d_to_2d(Vector3D(0, net_y, 0))
        net_bottom_end = self.project_3d_to_2d(Vector3D(net_width, net_y, 0))
        self.canvas.create_line(net_bottom_start[0], net_bottom_start[1],
                              net_bottom_end[0], net_bottom_end[1],
                              fill="white", width=3)
    
    def draw_net_post(self, bottom_pos, top_pos, width):
        """Draw a realistic net post"""
        # Post body
        self.canvas.create_line(bottom_pos[0], bottom_pos[1], 
                              top_pos[0], top_pos[1], 
                              fill="#8B4513", width=width)  # Brown color
        
        # Post base
        base_size = width + 4
        self.canvas.create_oval(bottom_pos[0] - base_size, bottom_pos[1] - base_size//2,
                              bottom_pos[0] + base_size, bottom_pos[1] + base_size//2,
                              fill="#654321", outline="#8B4513", width=2)
        
        # Post top
        self.canvas.create_oval(top_pos[0] - width//2, top_pos[1] - width//2,
                              top_pos[0] + width//2, top_pos[1] + width//2,
                              fill="#8B4513", outline="#654321", width=1)
    
    def draw_net_mesh(self, net_y, net_height, net_width):
        """Draw detailed net mesh pattern"""
        mesh_spacing_x = 20
        mesh_spacing_y = 8
        
        # Vertical mesh lines
        for i in range(0, int(net_width) + mesh_spacing_x, mesh_spacing_x):
            x = min(i, net_width)
            mesh_bottom = self.project_3d_to_2d(Vector3D(x, net_y, 0))
            mesh_top = self.project_3d_to_2d(Vector3D(x, net_y, net_height))
            self.canvas.create_line(mesh_bottom[0], mesh_bottom[1], 
                                  mesh_top[0], mesh_top[1],
                                  fill="#E6E6E6", width=1)
        
        # Horizontal mesh lines
        for j in range(0, int(net_height) + mesh_spacing_y, mesh_spacing_y):
            z = min(j, net_height)
            mesh_left = self.project_3d_to_2d(Vector3D(0, net_y, z))
            mesh_right = self.project_3d_to_2d(Vector3D(net_width, net_y, z))
            self.canvas.create_line(mesh_left[0], mesh_left[1],
                                  mesh_right[0], mesh_right[1],
                                  fill="#E6E6E6", width=1)
    
    def draw_court_surroundings(self):
        """Draw court surroundings for realism"""
        # Draw court boundary area (darker green)
        boundary_size = 100
        
        # Extended court area
        extended_corners = [
            (-boundary_size, -boundary_size),
            (WINDOW_WIDTH + boundary_size, -boundary_size),
            (WINDOW_WIDTH + boundary_size, WINDOW_HEIGHT + boundary_size),
            (-boundary_size, WINDOW_HEIGHT + boundary_size)
        ]
        
        self.canvas.create_polygon(extended_corners, 
                                 fill="#1F4F1F", outline="", 
                                 stipple="gray25")
        
        # Stadium/venue markings
        for i in range(4):
            for j in range(3):
                x = 50 + i * (WINDOW_WIDTH - 100) // 4
                y = 50 + j * (WINDOW_HEIGHT - 100) // 3
                self.canvas.create_text(x, y, text="🏸", fill="#2F4F2F", 
                                      font=("Arial", 20))
    
    def draw_player_detailed(self, player: Player, color: str = "blue"):
        """Draw detailed badminton player characters"""
        pos_2d = self.project_3d_to_2d(player.position)
        
        # Draw player shadow with realistic shape
        self.draw_player_shadow(player, pos_2d)
        
        # Draw player body parts
        self.draw_player_body(player, pos_2d, color)
        
        # Draw detailed racket
        self.draw_detailed_racket(player, pos_2d)
        
        # Draw player uniform details
        self.draw_player_uniform(player, pos_2d, color)
        
        # Draw player information
        self.draw_player_info(player, pos_2d)
        
        # Draw motion effects
        if player.velocity.length() > 50:
            self.draw_motion_effects(player, pos_2d)
    
    def draw_player_shadow(self, player: Player, pos_2d):
        """Draw realistic player shadow"""
        # Shadow size based on height and lighting
        shadow_width = 25
        shadow_height = 12
        shadow_offset_x = 3
        shadow_offset_y = 5
        
        # Multiple shadow layers for realism
        for i in range(3):
            alpha_factor = (3 - i) * 0.3
            shadow_size_w = shadow_width + i * 3
            shadow_size_h = shadow_height + i * 2
            
            gray_value = int(30 + i * 15)
            shadow_color = f"#{gray_value:02x}{gray_value:02x}{gray_value:02x}"
            
            self.canvas.create_oval(
                pos_2d[0] + shadow_offset_x - shadow_size_w, 
                pos_2d[1] + shadow_offset_y - shadow_size_h,
                pos_2d[0] + shadow_offset_x + shadow_size_w, 
                pos_2d[1] + shadow_offset_y + shadow_size_h,
                fill=shadow_color, outline=""
            )
    
    def draw_player_body(self, player: Player, pos_2d, color):
        """Draw detailed player body"""
        # Head
        head_pos = self.project_3d_to_2d(Vector3D(player.position.x, player.position.y, 35))
        head_size = 12
        
        # Head with hair
        self.canvas.create_oval(
            head_pos[0] - head_size, head_pos[1] - head_size,
            head_pos[0] + head_size, head_pos[1] + head_size,
            fill="#FDBCB4", outline="#8B4513", width=2  # Skin color
        )
        
        # Hair
        hair_size = head_size + 3
        self.canvas.create_oval(
            head_pos[0] - hair_size, head_pos[1] - hair_size,
            head_pos[0] + hair_size, head_pos[1] + hair_size - 6,
            fill="#654321", outline=""
        )
        
        # Eyes
        eye_size = 2
        left_eye_x = head_pos[0] - 4
        right_eye_x = head_pos[0] + 4
        eye_y = head_pos[1] - 2
        
        self.canvas.create_oval(left_eye_x - eye_size, eye_y - eye_size,
                              left_eye_x + eye_size, eye_y + eye_size,
                              fill="white", outline="black", width=1)
        self.canvas.create_oval(right_eye_x - eye_size, right_eye_y - eye_size,
                              right_eye_x + eye_size, eye_y + eye_size,
                              fill="white", outline="black", width=1)
        
        # Pupils
        self.canvas.create_oval(left_eye_x - 1, eye_y - 1,
                              left_eye_x + 1, eye_y + 1, fill="black")
        self.canvas.create_oval(right_eye_x - 1, eye_y - 1,
                              right_eye_x + 1, eye_y + 1, fill="black")
        
        # Torso (shirt)
        torso_pos = self.project_3d_to_2d(Vector3D(player.position.x, player.position.y, 20))
        torso_width = 16
        torso_height = 20
        
        shirt_color = color if color != "blue" else "#4169E1"
        if color == "red":
            shirt_color = "#DC143C"
        
        self.canvas.create_oval(
            torso_pos[0] - torso_width, torso_pos[1] - torso_height,
            torso_pos[0] + torso_width, torso_pos[1] + torso_height,
            fill=shirt_color, outline="white", width=2
        )
        
        # Arms
        self.draw_player_arms(player, torso_pos, shirt_color)
        
        # Legs (shorts and legs)
        self.draw_player_legs(player, pos_2d)
        
        # Shoes
        self.draw_player_shoes(player, pos_2d)
    
    def draw_player_arms(self, player: Player, torso_pos, shirt_color):
        """Draw player arms"""
        # Left arm
        left_shoulder = (torso_pos[0] - 12, torso_pos[1] - 5)
        left_elbow = (torso_pos[0] - 18, torso_pos[1] + 5)
        left_hand = (torso_pos[0] - 20, torso_pos[1] + 15)
        
        # Adjust arm position based on racket swing
        if player.animation_state == "hitting":
            swing_offset = math.sin(player.animation_time * 10) * 10
            left_hand = (left_hand[0] + swing_offset, left_hand[1] - swing_offset)
        
        self.canvas.create_line(left_shoulder[0], left_shoulder[1],
                              left_elbow[0], left_elbow[1], 
                              fill=shirt_color, width=6)
        self.canvas.create_line(left_elbow[0], left_elbow[1],
                              left_hand[0], left_hand[1],
                              fill="#FDBCB4", width=5)
        
        # Right arm (racket arm)
        right_shoulder = (torso_pos[0] + 12, torso_pos[1] - 5)
        right_elbow = (torso_pos[0] + 18, torso_pos[1] + 5)
        right_hand = (torso_pos[0] + 25, torso_pos[1] + 10)
        
        if player.animation_state == "hitting":
            swing_offset = math.sin(player.animation_time * 15) * 15
            right_hand = (right_hand[0] + swing_offset, right_hand[1] - swing_offset)
        
        self.canvas.create_line(right_shoulder[0], right_shoulder[1],
                              right_elbow[0], right_elbow[1],
                              fill=shirt_color, width=6)
        self.canvas.create_line(right_elbow[0], right_elbow[1],
                              right_hand[0], right_hand[1],
                              fill="#FDBCB4", width=5)
        
        # Hands
        hand_size = 3
        self.canvas.create_oval(left_hand[0] - hand_size, left_hand[1] - hand_size,
                              left_hand[0] + hand_size, left_hand[1] + hand_size,
                              fill="#FDBCB4", outline="black", width=1)
        self.canvas.create_oval(right_hand[0] - hand_size, right_hand[1] - hand_size,
                              right_hand[0] + hand_size, right_hand[1] + hand_size,
                              fill="#FDBCB4", outline="black", width=1)
    
    def draw_player_legs(self, player: Player, pos_2d):
        """Draw player legs"""
        # Shorts
        shorts_pos = self.project_3d_to_2d(Vector3D(player.position.x, player.position.y, 8))
        shorts_width = 14
        shorts_height = 8
        
        self.canvas.create_oval(
            shorts_pos[0] - shorts_width, shorts_pos[1] - shorts_height,
            shorts_pos[0] + shorts_width, shorts_pos[1] + shorts_height,
            fill="#1E90FF", outline="white", width=1  # Blue shorts
        )
        
        # Left leg
        left_hip = (shorts_pos[0] - 6, shorts_pos[1] + 5)
        left_knee = (pos_2d[0] - 8, pos_2d[1] - 15)
        left_ankle = (pos_2d[0] - 10, pos_2d[1] - 5)
        
        # Leg movement animation
        if player.velocity.length() > 20:
            leg_swing = math.sin(time.time() * 10) * 5
            left_knee = (left_knee[0] + leg_swing, left_knee[1])
            left_ankle = (left_ankle[0] + leg_swing * 2, left_ankle[1])
        
        self.canvas.create_line(left_hip[0], left_hip[1],
                              left_knee[0], left_knee[1],
                              fill="#FDBCB4", width=5)
        self.canvas.create_line(left_knee[0], left_knee[1],
                              left_ankle[0], left_ankle[1],
                              fill="#FDBCB4", width=5)
        
        # Right leg
        right_hip = (shorts_pos[0] + 6, shorts_pos[1] + 5)
        right_knee = (pos_2d[0] + 8, pos_2d[1] - 15)
        right_ankle = (pos_2d[0] + 10, pos_2d[1] - 5)
        
        if player.velocity.length() > 20:
            leg_swing = math.sin(time.time() * 10 + math.pi) * 5
            right_knee = (right_knee[0] + leg_swing, right_knee[1])
            right_ankle = (right_ankle[0] + leg_swing * 2, right_ankle[1])
        
        self.canvas.create_line(right_hip[0], right_hip[1],
                              right_knee[0], right_knee[1],
                              fill="#FDBCB4", width=5)
        self.canvas.create_line(right_knee[0], right_knee[1],
                              right_ankle[0], right_ankle[1],
                              fill="#FDBCB4", width=5)
    
    def draw_player_shoes(self, player: Player, pos_2d):
        """Draw player badminton shoes"""
        # Left shoe
        left_shoe_x = pos_2d[0] - 12
        left_shoe_y = pos_2d[1] - 3
        shoe_width = 8
        shoe_height = 4
        
        self.canvas.create_oval(
            left_shoe_x - shoe_width, left_shoe_y - shoe_height,
            left_shoe_x + shoe_width, left_shoe_y + shoe_height,
            fill="white", outline="black", width=2
        )
        
        # Right shoe
        right_shoe_x = pos_2d[0] + 12
        right_shoe_y = pos_2d[1] - 3
        
        self.canvas.create_oval(
            right_shoe_x - shoe_width, right_shoe_y - shoe_height,
            right_shoe_x + shoe_width, right_shoe_y + shoe_height,
            fill="white", outline="black", width=2
        )
        
        # Shoe details (stripes)
        for i in range(3):
            offset = i * 3 - 3
            self.canvas.create_line(left_shoe_x - 5, left_shoe_y + offset,
                                  left_shoe_x + 5, left_shoe_y + offset,
                                  fill="gray", width=1)
            self.canvas.create_line(right_shoe_x - 5, right_shoe_y + offset,
                                  right_shoe_x + 5, right_shoe_y + offset,
                                  fill="gray", width=1)
    
    def draw_detailed_racket(self, player: Player, pos_2d):
        """Draw a detailed badminton racket"""
        racket_angle_rad = math.radians(player.racket_angle)
        racket_length = 35
        
        # Calculate racket positions
        grip_start = Vector3D(player.position.x + 15, player.position.y, player.racket_height)
        grip_end = Vector3D(
            player.position.x + 15 + math.cos(racket_angle_rad) * racket_length * 0.4,
            player.position.y + math.sin(racket_angle_rad) * racket_length * 0.4,
            player.racket_height
        )
        shaft_end = Vector3D(
            player.position.x + 15 + math.cos(racket_angle_rad) * racket_length * 0.7,
            player.position.y + math.sin(racket_angle_rad) * racket_length * 0.7,
            player.racket_height + 2
        )
        head_center = Vector3D(
            player.position.x + 15 + math.cos(racket_angle_rad) * racket_length,
            player.position.y + math.sin(racket_angle_rad) * racket_length,
            player.racket_height + 3
        )
        
        # Project to 2D
        grip_start_2d = self.project_3d_to_2d(grip_start)
        grip_end_2d = self.project_3d_to_2d(grip_end)
        shaft_end_2d = self.project_3d_to_2d(shaft_end)
        head_center_2d = self.project_3d_to_2d(head_center)
        
        # Draw grip (handle)
        grip_color = "#8B4513"  # Brown
        self.canvas.create_line(
            grip_start_2d[0], grip_start_2d[1],
            grip_end_2d[0], grip_end_2d[1],
            fill=grip_color, width=8
        )
        
        # Grip tape pattern
        for i in range(3):
            offset_factor = i / 3.0
            grip_x = grip_start_2d[0] + (grip_end_2d[0] - grip_start_2d[0]) * offset_factor
            grip_y = grip_start_2d[1] + (grip_end_2d[1] - grip_start_2d[1]) * offset_factor
            self.canvas.create_line(grip_x - 3, grip_y, grip_x + 3, grip_y,
                                  fill="#654321", width=2)
        
        # Draw shaft
        shaft_color = "#C0C0C0"  # Silver
        self.canvas.create_line(
            grip_end_2d[0], grip_end_2d[1],
            shaft_end_2d[0], shaft_end_2d[1],
            fill=shaft_color, width=4
        )
        self.canvas.create_line(
            shaft_end_2d[0], shaft_end_2d[1],
            head_center_2d[0], head_center_2d[1],
            fill=shaft_color, width=3
        )
        
        # Draw racket head (frame)
        head_width = 15
        head_height = 20
        
        # Racket head oval
        self.canvas.create_oval(
            head_center_2d[0] - head_width, head_center_2d[1] - head_height,
            head_center_2d[0] + head_width, head_center_2d[1] + head_height,
            outline="#FF4500", width=4, fill=""  # Orange frame
        )
        
        # Draw strings in cross pattern
        string_color = "white"
        
        # Vertical strings
        for i in range(-2, 3):
            string_x = head_center_2d[0] + i * 4
            string_top_y = head_center_2d[1] - head_height * 0.8
            string_import tkinter as tk
from tkinter import messagebox, ttk
import math
import random
import time
import threading
from dataclasses import dataclass
from typing import List, Tuple, Optional, Dict, Any
from enum import Enum
import json
import os

# Game Constants
WINDOW_WIDTH = 1400
WINDOW_HEIGHT = 900
COURT_WIDTH = 600
COURT_HEIGHT = 400
NET_HEIGHT = 40
PLAYER_SIZE = 30
SHUTTLECOCK_SIZE = 8
GRAVITY = -200
AIR_RESISTANCE = 0.98
GROUND_BOUNCE_FACTOR = 0.6
GROUND_FRICTION = 0.8

# Physics Constants
PHYSICS_TIMESTEP = 0.016  # 60 FPS
MAX_VELOCITY = 500
MIN_VELOCITY = 0.1
SHUTTLECOCK_MASS = 0.005  # kg
RACKET_MASS = 0.3  # kg

# Game Balance Constants
SMASH_POWER_MULTIPLIER = 2.5
CLEAR_POWER_MULTIPLIER = 1.8
DRIVE_POWER_MULTIPLIER = 1.2
DROP_POWER_MULTIPLIER = 0.8
SERVE_POWER_MULTIPLIER = 1.0

# Animation Constants
HIT_ANIMATION_DURATION = 0.6
SERVE_ANIMATION_DURATION = 0.8
CELEBRATION_ANIMATION_DURATION = 2.0
PARTICLE_LIFETIME = 1.0

class ShotType(Enum):
    CLEAR = "clear"
    DROP = "drop"
    DRIVE = "drive"
    SMASH = "smash"
    SERVE = "serve"
    LIFT = "lift"
    NET_SHOT = "net_shot"
    BACKHAND = "backhand"

class GameState(Enum):
    MENU = "menu"
    PLAYING = "playing"
    PAUSED = "paused"
    GAME_OVER = "game_over"
    SERVING = "serving"
    RALLY = "rally"
    POINT_SCORED = "point_scored"
    SET_WON = "set_won"
    MATCH_WON = "match_won"

class PlayerType(Enum):
    HUMAN = "human"
    AI_EASY = "ai_easy"
    AI_MEDIUM = "ai_medium"
    AI_HARD = "ai_hard"
    AI_EXPERT = "ai_expert"

class WeatherCondition(Enum):
    SUNNY = "sunny"
    WINDY = "windy"
    HUMID = "humid"
    PERFECT = "perfect"

@dataclass
class Vector3D:
    x: float
    y: float
    z: float
    
    def __add__(self, other):
        return Vector3D(self.x + other.x, self.y + other.y, self.z + other.z)
    
    def __sub__(self, other):
        return Vector3D(self.x - other.x, self.y - other.y, self.z - other.z)
    
    def __mul__(self, scalar):
        return Vector3D(self.x * scalar, self.y * scalar, self.z * scalar)
    
    def __truediv__(self, scalar):
        if scalar == 0:
            return Vector3D(0, 0, 0)
        return Vector3D(self.x / scalar, self.y / scalar, self.z / scalar)
    
    def dot(self, other):
        return self.x * other.x + self.y * other.y + self.z * other.z
    
    def cross(self, other):
        return Vector3D(
            self.y * other.z - self.z * other.y,
            self.z * other.x - self.x * other.z,
            self.x * other.y - self.y * other.x
        )
    
    def length(self):
        return math.sqrt(self.x**2 + self.y**2 + self.z**2)
    
    def length_squared(self):
        return self.x**2 + self.y**2 + self.z**2
    
    def normalize(self):
        length = self.length()
        if length == 0:
            return Vector3D(0, 0, 0)
        return Vector3D(self.x/length, self.y/length, self.z/length)
    
    def distance_to(self, other):
        return (self - other).length()
    
    def lerp(self, other, t):
        return self + (other - self) * t

@dataclass
class PlayerStats:
    name: str
    wins: int = 0
    losses: int = 0
    sets_won: int = 0
    sets_lost: int = 0
    total_smashes: int = 0
    successful_smashes: int = 0
    total_shots: int = 0
    successful_shots: int = 0
    points_scored: int = 0
    aces: int = 0
    unforced_errors: int = 0
    forced_errors: int = 0
    net_kills: int = 0
    stamina: float = 100.0
    max_stamina: float = 100.0
    skill_level: int = 1
    experience: int = 0
    reaction_time: float = 0.5
    movement_speed: float = 100.0
    shot_accuracy: float = 0.7
    power_rating: float = 0.7
    consistency: float = 0.7
    court_coverage: float = 0.7
    mental_toughness: float = 0.7
    serve_accuracy: float = 0.7
    smash_power: float = 0.7
    drop_shot_finesse: float = 0.7
    
    def get_overall_rating(self) -> float:
        return (self.shot_accuracy + self.power_rating + self.consistency + 
                self.court_coverage + self.mental_toughness) / 5.0
    
    def update_experience(self, points_gained: int):
        self.experience += points_gained
        new_level = 1 + (self.experience // 1000)
        if new_level > self.skill_level:
            self.skill_level = new_level
            self.level_up_stats()
    
    def level_up_stats(self):
        improvement = 0.02
        self.shot_accuracy = min(1.0, self.shot_accuracy + improvement)
        self.power_rating = min(1.0, self.power_rating + improvement)
        self.consistency = min(1.0, self.consistency + improvement)
        self.court_coverage = min(1.0, self.court_coverage + improvement)
        self.max_stamina = min(150.0, self.max_stamina + 5)

@dataclass
class MatchStats:
    duration: float = 0.0
    total_rallies: int = 0
    longest_rally: int = 0
    shortest_rally: int = 999
    average_rally_length: float = 0.0
    total_shots: int = 0
    winners: int = 0
    errors: int = 0
    aces: int = 0
    service_errors: int = 0
    net_points: int = 0
    baseline_points: int = 0
    smash_winners: int = 0
    drop_shot_winners: int = 0

class Particle:
    def __init__(self, position: Vector3D, velocity: Vector3D, color: str, lifetime: float, size: float = 3):
        self.position = position
        self.velocity = velocity
        self.color = color
        self.lifetime = lifetime
        self.max_lifetime = lifetime
        self.size = size
        self.gravity = -100
        
    def update(self, dt: float):
        self.lifetime -= dt
        self.velocity.z += self.gravity * dt
        self.position = self.position + self.velocity * dt
        
    def is_alive(self) -> bool:
        return self.lifetime > 0
    
    def get_alpha(self) -> float:
        return self.lifetime / self.max_lifetime

class ParticleSystem:
    def __init__(self):
        self.particles: List[Particle] = []
        
    def emit(self, position: Vector3D, velocity: Vector3D, color: str, count: int = 10):
        for _ in range(count):
            particle_velocity = Vector3D(
                velocity.x + random.uniform(-50, 50),
                velocity.y + random.uniform(-50, 50),
                velocity.z + random.uniform(0, 100)
            )
            particle = Particle(position, particle_velocity, color, PARTICLE_LIFETIME)
            self.particles.append(particle)
    
    def emit_hit_effect(self, position: Vector3D, shot_type: ShotType):
        colors = {
            ShotType.SMASH: "red",
            ShotType.CLEAR: "blue",
            ShotType.DROP: "green",
            ShotType.DRIVE: "yellow",
            ShotType.SERVE: "white"
        }
        color = colors.get(shot_type, "white")
        
        for _ in range(15):
            angle = random.uniform(0, 2 * math.pi)
            speed = random.uniform(50, 150)
            velocity = Vector3D(
                math.cos(angle) * speed,
                math.sin(angle) * speed,
                random.uniform(50, 200)
            )
            particle = Particle(position, velocity, color, 0.8, random.uniform(2, 5))
            self.particles.append(particle)
    
    def emit_landing_effect(self, position: Vector3D):
        for _ in range(8):
            angle = random.uniform(0, 2 * math.pi)
            speed = random.uniform(20, 80)
            velocity = Vector3D(
                math.cos(angle) * speed,
                math.sin(angle) * speed,
                random.uniform(10, 50)
            )
            particle = Particle(position, velocity, "brown", 0.5, random.uniform(1, 3))
            self.particles.append(particle)
    
    def update(self, dt: float):
        self.particles = [p for p in self.particles if p.is_alive()]
        for particle in self.particles:
            particle.update(dt)

class Shuttlecock:
    def __init__(self, x: float, y: float, z: float = 50):
        self.position = Vector3D(x, y, z)
        self.velocity = Vector3D(0, 0, 0)
        self.angular_velocity = Vector3D(0, 0, 0)
        self.rotation = Vector3D(0, 0, 0)
        self.gravity = GRAVITY
        self.air_resistance = AIR_RESISTANCE
        self.spin = 0
        self.trail_positions = []
        self.max_trail_length = 15
        self.last_hit_time = 0
        self.hit_count = 0
        self.bounce_count = 0
        self.is_in_play = True
        self.last_player_hit = None
        self.shot_type_last_hit = None
        self.speed_history = []
        self.max_speed_recorded = 0
        
    def update(self, dt: float, weather: WeatherCondition = WeatherCondition.PERFECT):
        # Apply weather effects
        weather_factor = self.get_weather_factor(weather)
        
        # Apply physics
        self.velocity.z += self.gravity * dt
        
        # Air resistance with weather effects
        resistance = self.air_resistance * weather_factor
        self.velocity = self.velocity * resistance
        
        # Wind effects
        if weather == WeatherCondition.WINDY:
            wind_force = Vector3D(
                random.uniform(-20, 20),
                random.uniform(-10, 10),
                0
            )
            self.velocity = self.velocity + wind_force * dt
        
        # Update position
        old_pos = Vector3D(self.position.x, self.position.y, self.position.z)
        self.position = self.position + self.velocity * dt
        
        # Update rotation
        self.rotation = self.rotation + self.angular_velocity * dt
        
        # Add to trail
        if self.velocity.length() > 10:
            self.trail_positions.append(old_pos)
            if len(self.trail_positions) > self.max_trail_length:
                self.trail_positions.pop(0)
        
        # Record speed
        current_speed = self.velocity.length()
        self.speed_history.append(current_speed)
        if len(self.speed_history) > 60:  # Keep last 1 second of history
            self.speed_history.pop(0)
        
        if current_speed > self.max_speed_recorded:
            self.max_speed_recorded = current_speed
        
        # Bounce off ground
        if self.position.z <= 0:
            self.position.z = 0
            if self.velocity.z < -5:  # Only bounce if significant downward velocity
                self.velocity.z = abs(self.velocity.z) * GROUND_BOUNCE_FACTOR
                self.velocity.x *= GROUND_FRICTION
                self.velocity.y *= GROUND_FRICTION
                self.bounce_count += 1
                self.angular_velocity.x = random.uniform(-180, 180)
                self.angular_velocity.y = random.uniform(-180, 180)
            else:
                self.velocity = Vector3D(0, 0, 0)
                self.is_in_play = False
        
        # Update spin
        self.spin += dt * 360 * (1 + current_speed / 100)
        if self.spin > 360:
            self.spin -= 360
    
    def get_weather_factor(self, weather: WeatherCondition) -> float:
        factors = {
            WeatherCondition.PERFECT: 1.0,
            WeatherCondition.SUNNY: 0.98,
            WeatherCondition.HUMID: 1.02,
            WeatherCondition.WINDY: 0.95
        }
        return factors.get(weather, 1.0)
    
    def hit(self, player, shot_type: ShotType, power: float, direction: Vector3D, 
            spin_type: str = "none"):
        self.last_hit_time = time.time()
        self.hit_count += 1
        self.last_player_hit = player
        self.shot_type_last_hit = shot_type
        self.is_in_play = True
        
        # Calculate base velocity based on shot type
        power_multipliers = {
            ShotType.SMASH: SMASH_POWER_MULTIPLIER,
            ShotType.CLEAR: CLEAR_POWER_MULTIPLIER,
            ShotType.DRIVE: DRIVE_POWER_MULTIPLIER,
            ShotType.DROP: DROP_POWER_MULTIPLIER,
            ShotType.SERVE: SERVE_POWER_MULTIPLIER,
            ShotType.LIFT: 1.3,
            ShotType.NET_SHOT: 0.6,
            ShotType.BACKHAND: 0.9
        }
        
        multiplier = power_multipliers.get(shot_type, 1.0)
        base_speed = power * multiplier * (player.stats.power_rating)
        
        # Apply skill and stamina modifiers
        skill_modifier = 0.8 + (player.stats.skill_level / 10.0) * 0.4
        stamina_modifier = 0.6 + (player.stats.stamina / 100.0) * 0.4
        
        final_speed = base_speed * skill_modifier * stamina_modifier
        final_speed = max(50, min(MAX_VELOCITY, final_speed))
        
        # Set velocity based on direction and shot characteristics
        self.velocity = direction.normalize() * final_speed
        
        # Add shot-specific modifications
        if shot_type == ShotType.SMASH:
            self.velocity.z = max(50, self.velocity.z)  # Ensure downward trajectory
        elif shot_type == ShotType.CLEAR:
            self.velocity.z = max(200, abs(self.velocity.z))  # High trajectory
        elif shot_type == ShotType.DROP:
            self.velocity.z = min(-50, self.velocity.z)  # Ensure it drops
            self.velocity = self.velocity * 0.7  # Reduce overall speed
        elif shot_type == ShotType.DRIVE:
            self.velocity.z = max(-30, min(30, self.velocity.z))  # Keep it flat
        elif shot_type == ShotType.NET_SHOT:
            self.velocity = self.velocity * 0.5  # Very soft shot
        
        # Apply spin effects
        if spin_type == "topspin":
            self.angular_velocity.x = 720
            self.velocity.z -= 30
        elif spin_type == "backspin":
            self.angular_velocity.x = -720
            self.velocity.z += 30
        elif spin_type == "sidespin":
            self.angular_velocity.z = random.choice([-360, 360])
        
        # Add some random variation for realism
        accuracy_factor = player.stats.shot_accuracy
        if accuracy_factor < 1.0:
            error_factor = (1.0 - accuracy_factor) * 50
            self.velocity.x += random.uniform(-error_factor, error_factor)
            self.velocity.y += random.uniform(-error_factor, error_factor)
        
        # Clear trail on new hit
        self.trail_positions.clear()
    
    def get_predicted_landing_pos(self, time_limit: float = 5.0) -> Optional[Vector3D]:
        """Predict where shuttlecock will land using physics simulation"""
        if self.velocity.length() < MIN_VELOCITY:
            return None
        
        # Create temporary shuttlecock for simulation
        temp_pos = Vector3D(self.position.x, self.position.y, self.position.z)
        temp_vel = Vector3D(self.velocity.x, self.velocity.y, self.velocity.z)
        
        dt = 0.02
        time_elapsed = 0
        
        while temp_pos.z > 0 and time_elapsed < time_limit:
            # Apply same physics as update method
            temp_vel.z += self.gravity * dt
            temp_vel = temp_vel * self.air_resistance
            temp_pos = temp_pos + temp_vel * dt
            time_elapsed += dt
            
            if temp_vel.length() < MIN_VELOCITY:
                break
        
        return temp_pos if time_elapsed < time_limit else None
    
    def get_current_speed(self) -> float:
        return self.velocity.length()
    
    def get_average_speed(self) -> float:
        if not self.speed_history:
            return 0.0
        return sum(self.speed_history) / len(self.speed_history)

class Player:
    def __init__(self, name: str, x: float, y: float, player_type: PlayerType = PlayerType.HUMAN):
        self.stats = PlayerStats(name)
        self.player_type = player_type
        self.position = Vector3D(x, y, 0)
        self.target_position = Vector3D(x, y, 0)
        self.velocity = Vector3D(0, 0, 0)
        self.home_position = Vector3D(x, y, 0)
        self.facing_direction = Vector3D(0, 1, 0)
        
        # Animation and state
        self.animation_state = "idle"
        self.animation_time = 0
        self.racket_angle = 0
        self.racket_height = 15
        self.ready_to_hit = True
        self.last_shot_time = 0
        self.shot_power = 0
        self.charging_shot = False
        self.selected_shot_type = ShotType.CLEAR
        
        # Movement and physics
        self.max_speed = 150 + (self.stats.movement_speed * 50)
        self.acceleration = 300
        self.deceleration = 200
        self.reaction_time = self.stats.reaction_time
        
        # Game state
        self.current_side = "near" if y < 200 else "far"
        self.is_serving = False
        self.serves_remaining = 0
        self.consecutive_errors = 0
        self.momentum = 0.0  # -100 to 100, affects performance
        self.fatigue_level = 0.0  # 0 to 100, affects all stats
        
        # AI specific attributes
        self.last_decision_time = 0
        self.target_shuttlecock_pos = None
        self.predicted_landing = None
        self.strategy = "balanced"  # aggressive, defensive, balanced
        self.shot_preferences = {
            ShotType.CLEAR: 0.3,
            ShotType.DROP: 0.2,
            ShotType.DRIVE: 0.2,
            ShotType.SMASH: 0.2,
            ShotType.LIFT: 0.05,
            ShotType.NET_SHOT: 0.05
        }
        
        # Visual effects
        self.hit_effect_time = 0
        self.celebration_time = 0
        self.sweat_particles = []
        
    def update(self, dt: float, game_state=None):
        # Update position with smooth movement
        self.update_movement(dt)
        
        # Update animations
        self.update_animations(dt)
        
        # Update stamina and fatigue
        self.update_stamina_and_fatigue(dt)
        
        # Update momentum based on recent performance
        self.update_momentum()
        
        # Update shot charging
        if self.charging_shot:
            charge_rate = 80 + (self.stats.power_rating * 40)
            self.shot_power = min(100, self.shot_power + charge_rate * dt)
        
        # Update visual effects
        self.hit_effect_time = max(0, self.hit_effect_time - dt)
        self.celebration_time = max(0, self.celebration_time - dt)
        
        # Generate sweat particles when tired
        if self.stats.stamina < 30 and random.random() < 0.1:
            sweat_pos = Vector3D(
                self.position.x + random.uniform(-5, 5),
                self.position.y + random.uniform(-5, 5),
                20 + random.uniform(0, 10)
            )
            sweat_vel = Vector3D(
                random.uniform(-20, 20),
                random.uniform(-20, 20),
                random.uniform(-50, -10)
            )
            self.sweat_particles.append(Particle(sweat_pos, sweat_vel, "lightblue", 0.8, 2))
        
        # Update sweat particles
        self.sweat_particles = [p for p in self.sweat_particles if p.is_alive()]
        for particle in self.sweat_particles:
            particle.update(dt)
    
    def update_movement(self, dt: float):
        # Calculate movement toward target
        direction = self.target_position - self.position
        distance = direction.length()
        
        if distance > 2:
            # Apply acceleration/deceleration
            move_direction = direction.normalize()
            current_speed = self.velocity.length()
            
            if current_speed < self.max_speed:
                self.velocity = self.velocity + move_direction * self.acceleration * dt
            
            # Limit speed
            if self.velocity.length() > self.max_speed:
                self.velocity = self.velocity.normalize() * self.max_speed
            
            # Update position
            self.position = self.position + self.velocity * dt
            
            # Update facing direction
            if self.velocity.length() > 5:
                self.facing_direction = self.velocity.normalize()
            
            # Drain stamina when moving fast
            stamina_drain = (current_speed / self.max_speed) * 15 * dt
            self.stats.stamina = max(0, self.stats.stamina - stamina_drain)
            
        else:
            # Decelerate when near target
            self.velocity = self.velocity * (1 - self.deceleration * dt / 100)
            if self.velocity.length() < 5:
                self.velocity = Vector3D(0, 0, 0)
    
    def update_animations(self, dt: float):
        self.animation_time += dt
        
        if self.animation_state == "hitting":
            if self.animation_time > HIT_ANIMATION_DURATION:
                self.animation_state = "idle"
                self.ready_to_hit = True
        elif self.animation_state == "serving":
            if self.animation_time > SERVE_ANIMATION_DURATION:
                self.animation_state = "idle"
                self.ready_to_hit = True
        elif self.animation_state == "celebrating":
            if self.animation_time > CELEBRATION_ANIMATION_DURATION:
                self.animation_state = "idle"
        
        # Update racket position based on animation
        if self.animation_state == "hitting":
            progress = self.animation_time / HIT_ANIMATION_DURATION
            self.racket_angle = math.sin(progress * math.pi * 2) * 60
            self.racket_height = 15 + math.sin(progress * math.pi) * 20
        elif self.animation_state == "serving":
            progress = self.animation_time / SERVE_ANIMATION_DURATION
            self.racket_angle = -30 + progress * 90
            self.racket_height = 10 + progress * 30
        else:
            self.racket_angle = math.sin(time.time() * 2) * 5  # Idle sway
            self.racket_height = 15
    
    def update_stamina_and_fatigue(self, dt: float):
        # Recover stamina when not moving much
        if self.velocity.length() < 20:
            recovery_rate = 8 + (self.stats.mental_toughness * 5)
            self.stats.stamina = min(self.stats.max_stamina, 
                                   self.stats.stamina + recovery_rate * dt)
        
        # Calculate fatigue based on stamina
        self.fatigue_level = max(0, 100 - self.stats.stamina)
        
        # Fatigue affects all stats
        if self.fatigue_level > 50:
            fatigue_factor = (self.fatigue_level - 50) / 50.0 * 0.3
            self.max_speed = (150 + self.stats.movement_speed * 50) * (1 - fatigue_factor)
            self.reaction_time = self.stats.reaction_time * (1 + fatigue_factor)
    
    def update_momentum(self):
        # Momentum affects confidence and performance
        if self.momentum > 50:
            # Positive momentum boosts
            self.stats.shot_accuracy = min(1.0, self.stats.shot_accuracy * 1.1)
            self.stats.mental_toughness = min(1.0, self.stats.mental_toughness * 1.05)
        elif self.momentum < -50:
            # Negative momentum penalties
            self.stats.shot_accuracy *= 0.95
            self.stats.mental_toughness *= 0.98
        
        # Gradually decay momentum toward zero
        self.momentum *= 0.99
    
    def move_to(self, x: float, y: float):
        """Set target position for smooth movement"""
        self.target_position = Vector3D(
            max(0, min(COURT_WIDTH, x)),
            max(0, min(COURT_HEIGHT, y)),
            0
        )
    
    def move_relative(self, dx: float, dy: float):
        """Move relative to current position"""
        new_x = self.position.x + dx
        new_y = self.position.y + dy
        self.move_to(new_x, new_y)
    
    def return_to_base(self):
        """Return to home position"""
        self.move_to(self.home_position.x, self.home_position.y)
    
    def start_charging_shot(self, shot_type: ShotType = None):
        if self.ready_to_hit:
            self.charging_shot = True
            self.shot_power = 0
            if shot_type:
                self.selected_shot_type = shot_type
    
    def release_shot(self, shuttlecock: Shuttlecock = None, target_pos: Vector3D = None) -> dict:
        if not self.ready_to_hit or not self.charging_shot:
            return None
        
        self.charging_shot = False
        self.animation_state = "hitting"
        self.animation_time = 0
        self.ready_to_hit = False
        self.last_shot_time = time.time()
        self.stats.total_shots += 1
        self.hit_effect_time = 0.3
        
        # Calculate shot success based on multiple factors
        success_factors = [
            self.shot_power / 100.0,  # Charging time
            self.stats.stamina / 100.0,  # Energy level
            self.stats.shot_accuracy,  # Base skill
            1.0 - (self.fatigue_level / 200.0),  # Fatigue penalty
            1.0 + (self.momentum / 200.0),  # Momentum bonus/penalty
        ]
        
        success_chance = sum(success_factors) / len(success_factors)
        
        # Shot type specific modifiers
        if self.selected_shot_type == ShotType.SMASH:
            self.stats.total_smashes += 1
            success_chance *= 0.8  # Smashes are harder
        elif self.selected_shot_type == ShotType.DROP:
            success_chance *= 1.1  # Drop shots are easier
        
        # Calculate direction if target provided
        if shuttlecock and target_pos:
            direction = target_pos - shuttlecock.position
        else:
            # Default direction (across court)
            if self.current_side == "near":
                direction = Vector3D(0, 1, 0.3)
            else:
                direction = Vector3D(0, -1, 0.3)
        
        shot_info = {
            'type': self.selected_shot_type,
            'power': self.shot_power,
            'direction': direction,
            'success_chance': success_chance,
            'player': self
        }
        
        # Apply stamina cost
        stamina_cost = {
            ShotType.SMASH: 15,
            ShotType.CLEAR: 8,
            ShotType.DRIVE: 6,
            ShotType.DROP: 4,
            ShotType.SERVE: 5,
            ShotType.LIFT: 7,
            ShotType.NET_SHOT: 3
        }.get(self.selected_shot_type, 5)
        
        self.stats.stamina = max(0, self.stats.stamina - stamina_cost)
        self.shot_power = 0
        
        return shot_info
    
    def can_reach_shuttlecock(self, shuttlecock: Shuttlecock) -> bool:
        """Check if player can reach shuttlecock in time"""
        distance = self.position.distance_to(shuttlecock.position)
        time_to_reach = distance / self.max_speed
        
        # Estimate time until shuttlecock lands
        if shuttlecock.velocity.z <= 0 and shuttlecock.position.z > 0:
            time_to_land = shuttlecock.position.z / abs(shuttlecock.velocity.z)
            return time_to_reach <= time_to_land + self.reaction_time
        
        return distance < 60  # Within hitting range
    
    def get_optimal_position(self, shuttlecock: Shuttlecock) -> Vector3D:
        """Calculate optimal position to hit shuttlecock"""
        predicted_pos = shuttlecock.get_predicted_landing_pos()
        if predicted_pos:
            # Position slightly behind the predicted landing
            offset = Vector3D(0, -20 if self.current_side == "near" else 20, 0)
            return Vector3D(predicted_pos.x, predicted_pos.y, 0) + offset
        return self.position
    
    def celebrate(self):
        """Start celebration animation"""
        self.animation_state = "celebrating"
        self.animation_time = 0
        self.celebration_time = CELEBRATION_ANIMATION_DURATION
        self.momentum = min(100, self.momentum + 20)
    
    def show_frustration(self):
        """React to missing a shot or losing a point"""
        self.momentum = max(-100, self.momentum - 15)
        self.consecutive_errors += 1

class Court:
    def __init__(self):
        self.width = COURT_WIDTH
        self.height = COURT_HEIGHT
        self.net_height = NET_HEIGHT
        self.net_position = self.height // 2
        self.center_line = self.width // 2
        
        # Service areas
        self.service_lines = {
            'short_service_near': self.height * 0.25,
            'short_service_far': self.height * 0.75,
            'long_service_near': self.height * 0.15,
            'long_service_far': self.height * 0.85,
            'service_side_left': self.width * 0.25,
            'service_side_right': self.width * 0.75
        }
        
        # Court zones for AI strategy
        self.zones = {
            'front_left': (0, self.width//2, 0, self.height*0.3),
            'front_right': (self.width//2, self.width, 0, self.height*0.3),
            'mid_left': (0, self.width//2, self.height*0.3, self.height*0.7),
            'mid_right': (self.width//2, self.width, self.height*0.3, self.height*0.7),
            'back_left': (0, self.width//2, self.height*0.7, self.height),
            'back_right': (self.width//2, self.width, self.height*0.7, self.height)
        }
        
        # Court surface properties
        self.surface_type = "indoor"  # indoor, outdoor
        self.surface_speed = 1.0  # affects shuttlecock bounce
        self.court_temperature = 22.0  # Celsius
        self.humidity = 50.0  # percentage
        
    def is_in_bounds(self, x: float, y: float, is_serving: bool = False) -> bool:
        """Check if position is within court bounds"""
        if not (0 <= x <= self.width and 0 <= y <= self.height):
            return False
        
        if is_serving:
            return self.is_in_service_area(x, y)
        
        return True
    
    def is_in_service_area(self, x: float, y: float, serving_side: str = "near") -> bool:
        """Check if serve lands in correct service area"""
        if serving_side == "near":
            return (self.service_lines['short_service_far'] <= y <= self.service_lines['long_service_far'] and
                    0 <= x <= self.width)
        else:
            return (self.service_lines['long_service_near'] <= y <= self.service_lines['short_service_near'] and
                    0 <= x <= self.width)
    
    def get_court_side(self, y: float) -> str:
        """Determine which side of court the position is on"""
        return "near" if y < self.net_position else "far"
    
    def get_court_zone(self, x: float, y: float) -> str:
        """Get the zone name for a position"""
        for zone_name, (x1, x2, y1, y2) in self.zones.items():
            if x1 <= x <= x2 and y1 <= y <= y2:
                return zone_name
        return "unknown"
    
    def is_net_hit(self, shuttlecock_pos: Vector3D) -> bool:
        """Check if shuttlecock hit the net"""
        net_margin = 10
        return (abs(shuttlecock_pos.y - self.net_position) < net_margin and
                shuttlecock_pos.z < self.net_height and
                0 <= shuttlecock_pos.x <= self.width)
    
    def get_distance_to_net(self, position: Vector3D) -> float:
        """Get distance from position to net"""
        return abs(position.y - self.net_position)
    
    def get_court_center(self) -> Vector3D:
        """Get center position of court"""
        return Vector3D(self.width // 2, self.height // 2, 0)

class AI:
    def __init__(self, player: Player, difficulty: str = "medium"):
        self.player = player
        self.difficulty = difficulty
        self.setup_difficulty_parameters()
        
        # Decision making
        self.last_decision_time = 0
        self.decision_interval = self.reaction_delay
        self.current_strategy = "balanced"
        self.target_shuttlecock_pos = None
        self.predicted_landing = None
        
        # Learning and adaptation
        self.opponent_shot_history = []
        self.successful_shots = []
        self.failed_shots = []
        self.pattern_recognition = {}
        
        # Tactical awareness
        self.court_coverage_map = {}
        self.preferred_zones = ["mid_left", "mid_right"]
        self.weakness_zones = ["front_left", "front_right"]
        
        # Game state tracking
        self.rally_count = 0
        self.points_behind = 0
        self.pressure_level = 0.0
        self.last_shot_success = True
        
    def setup_difficulty_parameters(self):
        """Setup AI parameters based on difficulty level"""
        difficulty_settings = {
            "easy": {
                "reaction_delay": 0.8,
                "shot_accuracy": 0.6,
                "movement_speed": 0.7,
                "strategy_complexity": 0.5,
                "mistake_probability": 0.3,
                "stamina_management": 0.6
            },
            "medium": {
                "reaction_delay": 0.5,
                "shot_accuracy": 0.75,
                "movement_speed": 0.85,
                "strategy_complexity": 0.7,
                "mistake_probability": 0.15,
                "stamina_management": 0.8
            },
            "hard": {
                "reaction_delay": 0.3,
                "shot_accuracy": 0.9,
                "movement_speed": 0.95,
                "strategy_complexity": 0.9,
                "mistake_probability": 0.08,
                "stamina_management": 0.9
            },
            "expert": {
                "reaction_delay": 0.15,
                "shot_accuracy": 0.95,
                "movement_speed": 1.0,
                "strategy_complexity": 1.0,
                "mistake_probability": 0.03,
                "stamina_management": 1.0
            }
        }
        
        settings = difficulty_settings.get(self.difficulty, difficulty_settings["medium"])
        
        self.reaction_delay = settings["reaction_delay"]
        self.shot_accuracy = settings["shot_accuracy"]
        self.movement_speed_factor = settings["movement_speed"]
        self.strategy_complexity = settings["strategy_complexity"]
        self.mistake_probability = settings["mistake_probability"]
        self.stamina_management = settings["stamina_management"]
        
        # Apply settings to player stats
        self.player.stats.shot_accuracy *= self.shot_accuracy
        self.player.stats.reaction_time = self.reaction_delay
        self.player.max_speed *= self.movement_speed_factor
    
    def update(self, game_state, dt: float):
        """Main AI update loop"""
        current_time = time.time()
        
        # Only make decisions at intervals based on reaction time
        if current_time - self.last_decision_time < self.decision_interval:
            return
        
        self.last_decision_time = current_time
        
        # Update game state awareness
        self.update_game_awareness(game_state)
        
        # Get shuttlecock information
        shuttlecock = game_state.shuttlecock
        if shuttlecock is None or not shuttlecock.is_in_play:
            self.handle_no_shuttlecock(game_state)
            return
        
        # Analyze current situation
        situation = self.analyze_situation(shuttlecock, game_state)
        
        # Make strategic decisions
        if situation["should_move"]:
            self.decide_movement(shuttlecock, situation)
        
        if situation["should_hit"]:
            self.decide_shot(shuttlecock, game_state, situation)
    
    def update_game_awareness(self, game_state):
        """Update AI's understanding of the game state"""
        self.rally_count = getattr(game_state, 'rally_count', 0)
        
        # Calculate pressure level based on score difference
        if hasattr(game_state, 'score'):
            player_score = game_state.score[1] if game_state.player2 == self.player else game_state.score[0]
            opponent_score = game_state.score[0] if game_state.player2 == self.player else game_state.score[1]
            self.points_behind = opponent_score - player_score
            
            # Increase pressure when behind
            self.pressure_level = max(0, self.points_behind * 0.1)
        
        # Adjust strategy based on pressure
        if self.pressure_level > 0.5:
            self.current_strategy = "aggressive"
        elif self.pressure_level < -0.3:
            self.current_strategy = "defensive"
        else:
            self.current_strategy = "balanced"
    
    def analyze_situation(self, shuttlecock: Shuttlecock, game_state) -> dict:
        """Analyze current game situation"""
        situation = {
            "shuttlecock_speed": shuttlecock.get_current_speed(),
            "shuttlecock_height": shuttlecock.position.z,
            "distance_to_shuttlecock": self.player.position.distance_to(shuttlecock.position),
            "time_to_reach": 0,
            "should_move": False,
            "should_hit": False,
            "hit_difficulty": 0,
            "opponent_position": None
        }
        
        # Calculate time to reach shuttlecock
        if situation["distance_to_shuttlecock"] > 0:
            situation["time_to_reach"] = situation["distance_to_shuttlecock"] / self.player.max_speed
        
        # Predict shuttlecock landing
        self.predicted_landing = shuttlecock.get_predicted_landing_pos()
        
        # Determine if we should move
        situation["should_move"] = (
            self.predicted_landing is not None and
            self.player.position.distance_to(self.predicted_landing) > 30
        )
        
        # Determine if we should hit
        situation["should_hit"] = (
            situation["distance_to_shuttlecock"] < 50 and
            shuttlecock.position.z < 120 and
            shuttlecock.velocity.length() > 10 and
            self.player.ready_to_hit
        )
        
        # Calculate hit difficulty
        if situation["should_hit"]:
            difficulty_factors = [
                situation["shuttlecock_speed"] / 300.0,
                max(0, situation["shuttlecock_height"] - 30) / 100.0,
                situation["distance_to_shuttlecock"] / 50.0,
                self.player.fatigue_level / 100.0
            ]
            situation["hit_difficulty"] = sum(difficulty_factors) / len(difficulty_factors)
        
        return situation
    
    def decide_movement(self, shuttlecock: Shuttlecock, situation: dict):
        """Decide where to move based on shuttlecock and strategy"""
        if self.predicted_landing is None:
            return
        
        # Calculate optimal position with strategy considerations
        target_pos = self.calculate_optimal_position(shuttlecock, situation)
        
        # Add some error based on AI skill level
        if self.shot_accuracy < 1.0:
            error_range = (1.0 - self.shot_accuracy) * 40
            target_pos.x += random.uniform(-error_range, error_range)
            target_pos.y += random.uniform(-error_range, error_range)
        
        # Ensure position is within court bounds
        target_pos.x = max(20, min(COURT_WIDTH - 20, target_pos.x))
        target_pos.y = max(20, min(COURT_HEIGHT - 20, target_pos.y))
        
        self.player.move_to(target_pos.x, target_pos.y)
    
    def calculate_optimal_position(self, shuttlecock: Shuttlecock, situation: dict) -> Vector3D:
        """Calculate the best position to be in"""
        if self.predicted_landing is None:
            return self.player.position
        
        # Base position: slightly behind predicted landing
        base_offset = 25
        if self.player.current_side == "near":
            offset_y = -base_offset
        else:
            offset_y = base_offset
        
        optimal_pos = Vector3D(
            self.predicted_landing.x,
            self.predicted_landing.y + offset_y,
            0
        )
        
        # Adjust based on strategy
        if self.current_strategy == "aggressive":
            # Move closer to net for aggressive play
            net_y = COURT_HEIGHT // 2
            if optimal_pos.y < net_y:
                optimal_pos.y = min(optimal_pos.y + 30, net_y - 40)
            else:
                optimal_pos.y = max(optimal_pos.y - 30, net_y + 40)
        
        elif self.current_strategy == "defensive":
            # Stay back for defensive play
            if self.player.current_side == "near":
                optimal_pos.y = min(optimal_pos.y, COURT_HEIGHT * 0.3)
            else:
                optimal_pos.y = max(optimal_pos.y, COURT_HEIGHT * 0.7)
        
        return optimal_pos
    
    def decide_shot(self, shuttlecock: Shuttlecock, game_state, situation: dict):
        """Decide what type of shot to make"""
        if not self.player.ready_to_hit:
            return
        
        # Choose shot type based on situation and strategy
        shot_type = self.choose_shot_type(shuttlecock, situation)
        
        # Calculate target position for shot
        target_pos = self.choose_target_position(shuttlecock, shot_type, game_state)
        
        # Execute the shot
        self.execute_shot(shot_type, shuttlecock, target_pos, situation)
    
    def choose_shot_type(self, shuttlecock: Shuttlecock, situation: dict) -> ShotType:
        """Choose the best shot type for the situation"""
        height = shuttlecock.position.z
        speed = situation["shuttlecock_speed"]
        distance = situation["distance_to_shuttlecock"]
        
        # Shot type probabilities based on situation
        shot_probabilities = {}
        
        # High shuttlecock - good for smashing
        if height > 80 and self.player.stats.stamina > 40:
            shot_probabilities[ShotType.SMASH] = 0.4
            shot_probabilities[ShotType.CLEAR] = 0.3
            shot_probabilities[ShotType.DROP] = 0.2
            shot_probabilities[ShotType.DRIVE] = 0.1
        
        # Medium height - versatile options
        elif 30 < height <= 80:
            shot_probabilities[ShotType.CLEAR] = 0.3
            shot_probabilities[ShotType.DRIVE] = 0.25
            shot_probabilities[ShotType.DROP] = 0.25
            shot_probabilities[ShotType.SMASH] = 0.15
            shot_probabilities[ShotType.LIFT] = 0.05
        
        # Low shuttlecock - limited options
        else:
            shot_probabilities[ShotType.LIFT] = 0.4
            shot_probabilities[ShotType.NET_SHOT] = 0.25
            shot_probabilities[ShotType.DRIVE] = 0.25
            shot_probabilities[ShotType.DROP] = 0.1
        
        # Adjust based on strategy
        if self.current_strategy == "aggressive":
            shot_probabilities[ShotType.SMASH] = shot_probabilities.get(ShotType.SMASH, 0) * 1.5
            shot_probabilities[ShotType.DROP] = shot_probabilities.get(ShotType.DROP, 0) * 1.3
        elif self.current_strategy == "defensive":
            shot_probabilities[ShotType.CLEAR] = shot_probabilities.get(ShotType.CLEAR, 0) * 1.4
            shot_probabilities[ShotType.LIFT] = shot_probabilities.get(ShotType.LIFT, 0) * 1.2
        
        # Add random mistakes based on difficulty
        if random.random() < self.mistake_probability:
            # Choose a less optimal shot
            return random.choice(list(ShotType))
        
        # Choose shot based on probabilities
        return self.weighted_choice(shot_probabilities)
    
    def choose_target_position(self, shuttlecock: Shuttlecock, shot_type: ShotType, game_state) -> Vector3D:
        """Choose where to aim the shot"""
        opponent = game_state.player1 if game_state.player2 == self.player else game_state.player2
        
        # Base target: opposite side of court
        if self.player.current_side == "near":
            base_target_y = COURT_HEIGHT * 0.8
        else:
            base_target_y = COURT_HEIGHT * 0.2
        
        base_target = Vector3D(COURT_WIDTH // 2, base_target_y, 0)
        
        # Adjust target based on shot type
        if shot_type == ShotType.SMASH:
            # Aim for corners or away from opponent
            if opponent.position.x < COURT_WIDTH // 2:
                base_target.x = COURT_WIDTH * 0.8
            else:
                base_target.x = COURT_WIDTH * 0.2
        
        elif shot_type == ShotType.DROP:
            # Aim for front court
            if self.player.current_side == "near":
                base_target.y = COURT_HEIGHT * 0.6
            else:
                base_target.y = COURT_HEIGHT * 0.4
        
        elif shot_type == ShotType.CLEAR:
            # Aim for back court
            if self.player.current_side == "near":
                base_target.y = COURT_HEIGHT * 0.9
            else:
                base_target.y = COURT_HEIGHT * 0.1
        
        elif shot_type == ShotType.NET_SHOT:
            # Aim close to net
            base_target.y = COURT_HEIGHT // 2 + (10 if self.player.current_side == "near" else -10)
        
        # Add strategic positioning - avoid opponent
        opponent_distance = base_target.distance_to(opponent.position)
        if opponent_distance < 100:
            # Move target away from opponent
            away_vector = (base_target - opponent.position).normalize()
            base_target = base_target + away_vector * 50
        
        # Add some randomness for unpredictability
        accuracy_error = (1.0 - self.shot_accuracy) * 30
        base_target.x += random.uniform(-accuracy_error, accuracy_error)
        base_target.y += random.uniform(-accuracy_error, accuracy_error)
        
        # Ensure target is within bounds
        base_target.x = max(20, min(COURT_WIDTH - 20, base_target.x))
        base_target.y = max(20, min(COURT_HEIGHT - 20, base_target.y))
        
        return base_target
    
    def execute_shot(self, shot_type: ShotType, shuttlecock: Shuttlecock, target_pos: Vector3D, situation: dict):
        """Execute the chosen shot"""
        # Start charging shot
        self.player.start_charging_shot(shot_type)
        
        # Calculate charge time based on shot type and AI skill
        base_charge_times = {
            ShotType.SMASH: 0.8,
            ShotType.CLEAR: 0.6,
            ShotType.DRIVE: 0.4,
            ShotType.DROP: 0.5,
            ShotType.LIFT: 0.6,
            ShotType.NET_SHOT: 0.3
        }
        
        charge_time = base_charge_times.get(shot_type, 0.5) * self.shot_accuracy
        
        # Add timing variation for realism
        charge_time += random.uniform(-0.1, 0.1)
        charge_time = max(0.1, charge_time)
        
        # Execute shot after delay
        def delayed_shot_execution():
            time.sleep(charge_time)
            if self.player.charging_shot:  # Make sure player is still charging
                shot_info = self.player.release_shot(shuttlecock, target_pos)
                if shot_info:
                    self.record_shot_attempt(shot_type, target_pos, situation)
        
        # Start shot execution in separate thread
        threading.Thread(target=delayed_shot_execution, daemon=True).start()
    
    def record_shot_attempt(self, shot_type: ShotType, target_pos: Vector3D, situation: dict):
        """Record shot for learning and analysis"""
        shot_record = {
            'type': shot_type,
            'target': target_pos,
            'situation': situation,
            'timestamp': time.time(),
            'strategy': self.current_strategy
        }
        
        # Store for later analysis
        if len(self.successful_shots) > 100:
            self.successful_shots.pop(0)
        self.successful_shots.append(shot_record)
    
    def weighted_choice(self, choices: dict):
        """Make a weighted random choice from a dictionary of options"""
        if not choices:
            return ShotType.CLEAR
        
        # Normalize probabilities
        total = sum(choices.values())
        if total == 0:
            return random.choice(list(choices.keys()))
        
        normalized = {k: v/total for k, v in choices.items()}
        
        # Make choice
        rand = random.random()
        cumulative = 0
        
        for choice, probability in normalized.items():
            cumulative += probability
            if rand <= cumulative:
                return choice
        
        return list(choices.keys())[-1]
    
    def handle_no_shuttlecock(self, game_state):
        """Handle behavior when shuttlecock is not in play"""
        # Return to optimal court position
        if hasattr(game_state, 'is_serving') and game_state.is_serving:
            # Move to serving position
            if self.player.is_serving:
                serve_pos = Vector3D(COURT_WIDTH // 2, COURT_HEIGHT * 0.15, 0)
            else:
                serve_pos = Vector3D(COURT_WIDTH // 2, COURT_HEIGHT * 0.85, 0)
            self.player.move_to(serve_pos.x, serve_pos.y)
        else:
            # Return to base position
            self.player.return_to_base()

class GameRenderer:
    def __init__(self, canvas: tk.Canvas):
        self.canvas = canvas
        self.camera_position = Vector3D(COURT_WIDTH // 2, -100, 200)
        self.camera_target = Vector3D(COURT_WIDTH // 2, COURT_HEIGHT // 2, 0)
        self.camera_angle = 0
        self.camera_tilt = 0.3
        self.zoom = 1.0
        self.field_of_view = 60
        
        # Visual effects
        self.screen_shake = 0
        self.flash_effect = 0
        self.slow_motion_factor = 1.0
        
        # Render settings
        self.show_trails = True
        self.show_stats = True
        self.show_effects = True
        self.render_shadows = True
        self.render_particles = True
        
        # Colors and themes
        self.court_color = "darkgreen"
        self.line_color = "white"
        self.net_color = "white"
        self.background_color = "black"
        
    def clear_screen(self):
        """Clear the canvas"""
        self.canvas.delete("all")
        
        # Apply screen effects
        if self.flash_effect > 0:
            flash_intensity = int(255 * self.flash_effect)
            flash_color = f"#{flash_intensity:02x}{flash_intensity:02x}{flash_intensity:02x}"
            self.canvas.create_rectangle(0, 0, WINDOW_WIDTH, WINDOW_HEIGHT, 
                                       fill=flash_color, outline="")
            self.flash_effect = max(0, self.flash_effect - 0.1)
    
    def project_3d_to_2d(self, pos: Vector3D) -> Tuple[float, float]:
        """Enhanced 3D to 2D projection with perspective"""
        # Apply screen shake
        shake_x = random.uniform(-self.screen_shake, self.screen_shake)
        shake_y = random.uniform(-self.screen_shake, self.screen_shake)
        
        # Translate to camera space
        relative_pos = pos - self.camera_position
        
        # Apply camera rotation
        cos_angle = math.cos(self.camera_angle)
        sin_angle = math.sin(self.camera_angle)
        
        rotated_x = relative_pos.x * cos_angle - relative_pos.y * sin_angle
        rotated_y = relative_pos.x * sin_angle + relative_pos.y * cos_angle
        rotated_z = relative_pos.z
        
        # Apply tilt
        cos_tilt = math.cos(self.camera_tilt)
        sin_tilt = math.sin(self.camera_tilt)
        
        final_y = rotated_y * cos_tilt - rotated_z * sin_tilt
        final_z = rotated_y * sin_tilt + rotated_z * cos_tilt
        
        # Perspective projection
        if final_z > 1:
            fov_scale = math.tan(math.radians(self.field_of_view / 2))
            screen_x = (rotated_x / final_z) * WINDOW_HEIGHT * fov_scale * self.zoom + WINDOW_WIDTH // 2
            screen_y = (final_y / final_z) * WINDOW_HEIGHT * fov_scale * self.zoom + WINDOW_HEIGHT // 2
        else:
            screen_x = WINDOW_WIDTH // 2
            screen_y = WINDOW_HEIGHT // 2
        
        return screen_x + shake_x, screen_y + shake_y
    
    def draw_background(self):
        """Draw background gradient"""
        # Create gradient effect
        for i in range(0, WINDOW_HEIGHT, 10):
            intensity = int(20 + (i / WINDOW_HEIGHT) * 40)
            color = f"#{intensity:02x}{intensity:02x}{intensity+10:02x}"
            self.canvas.create_rectangle(0, i, WINDOW_WIDTH, i + 10, 
                                       fill=color, outline="")
    
    def draw_court_detailed(self, court: Court):
        """Draw detailed court with all lines and zones"""
        # Draw court base
        court_corners = [
            Vector3D(0, 0, 0),
            Vector3D(court.width, 0, 0), 
            Vector3D(court.width, court.height, 0),
            Vector3D(0, court.height, 0)
        ]
        
        projected_corners = [self.project_3d_to_2d(corner) for corner in court_corners]
        
        # Main court area
        self.canvas.create_polygon(
            [coord for point in projected_corners for coord in point],
            fill=self.court_color, outline=self.line_color, width=4
        )
        
        # Draw court lines
        self.draw_court_lines(court)
        
        # Draw net structure
        self.draw_net_structure(court)
        
        # Draw court zones (faintly)
        if self.show_stats:
            self.draw_court_zones(court)
    
    def draw_court_lines(self, court: Court):
        """Draw all court lines"""
        # Service lines
        service_lines = [
            ('short_service_near', 'yellow'),
            ('short_service_far', 'yellow'),
            ('long_service_near', 'lightblue'),
            ('long_service_far', 'lightblue')
        ]
        
        for line_name, color in service_lines:
            if line_name in court.service_lines:
                y = court.service_lines[line_name]
                start = self.project_3d_to_2d(Vector3D(0, y, 0))
                end = self.project_3d_to_2d(Vector3D(court.width, y, 0))
                self.canvas.create_line(start[0], start[1], end[0], end[1],
                                      fill=color, width=2, dash=(8, 4))
        
        # Center line
        center_start = self.project_3d_to_2d(Vector3D(court.center_line, 0, 0))
        center_end = self.project_3d_to_2d(Vector3D(court.center_line, court.height, 0))
        self.canvas.create_line(center_start[0], center_start[1], center_end[0], center_end[1],
                              fill=self.line_color, width=3)
        
        # Side service lines
        left_service = self.project_3d_to_2d(Vector3D(court.service_lines.get('service_side_left', court.width * 0.25), 0, 0))
        left_service_end = self.project_3d_to_2d(Vector3D(court.service_lines.get('service_side_left', court.width * 0.25), court.height, 0))
        self.canvas.create_line(left_service[0], left_service[1], left_service_end[0], left_service_end[1],
                              fill='orange', width=2, dash=(5, 5))
        
        right_service = self.project_3d_to_2d(Vector3D(court.service_lines.get('service_side_right', court.width * 0.75), 0, 0))
        right_service_end = self.project_3d_to_2d(Vector3D(court.service_lines.get('service_side_right', court.width * 0.75), court.height, 0))
        self.canvas.create_line(right_service[0], right_service[1], right_service_end[0], right_service_end[1],
                              fill='orange', width=2, dash=(5, 5))
    
    def draw_net_structure(self, court: Court):
        """Draw detailed net structure"""
        net_y = court.net_position
        net_height = court.net_height
        
        # Net posts
        left_post_bottom = self.project_3d_to_2d(Vector3D(-10, net_y, 0))
        left_post_top = self.project_3d_to_2d(Vector3D(-10, net_y, net_height + 20))
        right_post_bottom = self.project_3d_to_2d(Vector3D(court.width + 10, net_y, 0))
        right_post_top = self.project_3d_to_2d(Vector3D(court.width + 10, net_y, net_height + 20))
        
        self.canvas.create_line(left_post_bottom[0], left_post_bottom[1], 
                              left_post_top[0], left_post_top[1], fill="brown", width=6)
        self.canvas.create_line(right_post_bottom[0], right_post_bottom[1], 
                              right_post_top[0], right_post_top[1], fill="brown", width=6)
        
        # Net base and top
        net_bottom_start = self.project_3d_to_2d(Vector3D(0, net_y, 0))
        net_bottom_end = self.project_3d_to_2d(Vector3D(court.width, net_y, 0))
        net_top_start = self.project_3d_to_2d(Vector3D(0, net_y, net_height))
        net_top_end = self.project_3d_to_2d(Vector3D(court.width, net_y, net_height))
        
        self.canvas.create_line(net_bottom_start[0], net_bottom_start[1], 
                              net_bottom_end[0], net_bottom_end[1], fill=self.net_color, width=4)
        self.canvas.create_line(net_top_start[0], net_top_start[1], 
                              net_top_end[0], net_top_end[1], fill=self.net_color, width=4)
        
        # Net mesh
        mesh_segments = 15
        for i in range(mesh_segments + 1):
            x = i * court.width / mesh_segments
            mesh_bottom = self.project_3d_to_2d(Vector3D(x, net_y, 0))
            mesh_top = self.project_3d_to_2d(Vector3D(x, net_y, net_height))
            self.canvas.create_line(mesh_bottom[0], mesh_bottom[1], mesh_top[0], mesh_top[1],
                                  fill="lightgray", width=1)
        
        # Horizontal mesh lines
        for i in range(1, 4):
            z = i * net_height / 4
            mesh_start = self.project_3d_to_2d(Vector3D(0, net_y, z))
            mesh_end = self.project_3d_to_2d(Vector3D(court.width, net_y, z))
            self.canvas.create_line(mesh_start[0], mesh_start[1], mesh_end[0], mesh_end[1],
                                  fill="lightgray", width=1)
    
    def draw_court_zones(self, court: Court):
        """Draw faint zone indicators"""
        zone_colors = {
            'front_left': 'rgba(255,0,0,0.1)',
            'front_right': 'rgba(0,255,0,0.1)', 
            'mid_left': 'rgba(0,0,255,0.1)',
            'mid_right': 'rgba(255,255,0,0.1)',
            'back_left': 'rgba(255,0,255,0.1)',
            'back_right': 'rgba(0,255,255,0.1)'
        }
        
        for zone_name, (x1, x2, y1, y2) in court.zones.items():
            if zone_name in zone_colors:
                corners = [
                    self.project_3d_to_2d(Vector3D(x1, y1, 1)),
                    self.project_3d_to_2d(Vector3D(x2, y1, 1)),
                    self.project_3d_to_2d(Vector3D(x2, y2, 1)),
                    self.project_3d_to_2d(Vector3D(x1, y2, 1))
                ]
                
                # Draw zone outline only
                points = [coord for point in corners for coord in point]
                self.canvas.create_polygon(points, fill="", outline="gray", width=1, dash=(2, 4))
    
    def draw_player_detailed(self, player: Player, color: str = "blue"):
        """Draw detailed player with animations and effects"""
        pos_2d = self.project_3d_to_2d(player.position)
        
        # Draw player shadow
        shadow_size = 20 - (player.position.z / 10)
        shadow_alpha = max(0.2, 1.0 - player.position.z / 100.0)
        self.canvas.create_oval(
            pos_2d[0] - shadow_size, pos_2d[1] - shadow_size,
            pos_2d[0] + shadow_size, pos_2d[1] + shadow_size,
            fill="gray", outline="", stipple="gray50"
        )
        
        # Player body with animation
        body_size = 12
        if player.animation_state == "hitting":
            body_size += math.sin(player.animation_time * 10) * 3
        elif player.animation_state == "celebrating":
            body_size += math.sin(player.animation_time * 8) * 5
            color = "gold"
        
        # Body
        self.canvas.create_oval(
            pos_2d[0] - body_size, pos_2d[1] - body_size,
            pos_2d[0] + body_size, pos_2d[1] + body_size,
            fill=color, outline="black", width=2
        )
        
        # Head
        head_pos = self.project_3d_to_2d(Vector3D(player.position.x, player.position.y, 25))
        head_size = 8
        self.canvas.create_oval(
            head_pos[0] - head_size, head_pos[1] - head_size,
            head_pos[0] + head_size, head_pos[1] + head_size,
            fill="peachpuff", outline="black", width=2
        )
        
        # Draw racket with detailed animation
        self.draw_racket(player, pos_2d)
        
        # Player information
        self.draw_player_info(player, pos_2d)
        
        # Visual effects
        if player.hit_effect_time > 0:
            self.draw_hit_effect(player, pos_2d)
        
        # Sweat particles
        if self.render_particles:
            for particle in player.sweat_particles:
                self.draw_particle(particle)
    
    def draw_racket(self, player: Player, player_pos_2d: Tuple[float, float]):
        """Draw detailed racket with animation"""
        racket_angle_rad = math.radians(player.racket_angle)
        racket_length = 30
        
        # Calculate racket position
        racket_handle_start = Vector3D(player.position.x, player.position.y, player.racket_height)
        racket_handle_end = Vector3D(
            player.position.x + math.cos(racket_angle_rad) * racket_length * 0.6,
            player.position.y + math.sin(racket_angle_rad) * racket_length * 0.6,
            player.racket_height + 5
        )
        racket_head_center = Vector3D(
            player.position.x + math.cos(racket_angle_rad) * racket_length,
            player.position.y + math.sin(racket_angle_rad) * racket_length,
            player.racket_height + 8
        )
        
        # Project to 2D
        handle_start_2d = self.project_3d_to_2d(racket_handle_start)
        handle_end_2d = self.project_3d_to_2d(racket_handle_end)
        head_center_2d = self.project_3d_to_2d(racket_head_center)
        
        # Draw handle
        handle_width = 4 if player.animation_state != "hitting" else 6
        self.canvas.create_line(
            handle_start_2d[0], handle_start_2d[1],
            handle_end_2d[0], handle_end_2d[1],
            fill="brown", width=handle_width
        )
        
        # Draw racket head
        head_size = 12
        if player.animation_state == "hitting":
            head_size += math.sin(player.animation_time * 15) * 3
        
        self.canvas.create_oval(
            head_center_2d[0] - head_size, head_center_2d[1] - head_size,
            head_center_2d[0] + head_size, head_center_2d[1] + head_size,
            outline="orange", width=3, fill=""
        )
        
        # Draw strings
        string_count = 8
        for i in range(string_count):
            angle = i * (2 * math.pi / string_count)
            string_start_x = head_center_2d[0] + math.cos(angle) * head_size * 0.3
            string_start_y = head_center_2d[1] + math.sin(angle) * head_size * 0.3
            string_end_x = head_center_2d[0] + math.cos(angle) * head_size * 0.8
            string_end_y = head_center_2d[1] + math.sin(angle) * head_size * 0.8
            
            self.canvas.create_line(
                string_start_x, string_start_y, string_end_x, string_end_y,
                fill="white", width=1
            )
    
    def draw_player_info(self, player: Player, pos_2d: Tuple[float, float]):
        """Draw player information UI"""
        # Name
        name_color = "white" if player.momentum >= 0 else "red"
        if player.momentum > 50:
            name_color = "yellow"
        
        self.canvas.create_text(
            pos_2d[0], pos_2d[1] - 50,
            text=player.stats.name, fill=name_color, 
            font=("Arial", 12, "bold")
        )
        
        # Stamina bar
        stamina_width = 40
        stamina_height = 6
        stamina_x = pos_2d[0] - stamina_width // 2
        stamina_y = pos_2d[1] - 35
        
        # Background
        self.canvas.create_rectangle(
            stamina_x, stamina_y, stamina_x + stamina_width, stamina_y + stamina_height,
            fill="red", outline="black", width=1
        )
        
        # Stamina fill
        stamina_fill = (player.stats.stamina / player.stats.max_stamina) * stamina_width
        stamina_color = "green"
        if player.stats.stamina < 30:
            stamina_color = "red"
        elif player.stats.stamina < 60:
            stamina_color = "yellow"
        
        self.canvas.create_rectangle(
            stamina_x, stamina_y, stamina_x + stamina_fill, stamina_y + stamina_height,
            fill=stamina_color, outline=""
        )
        
        # Power charging indicator
        if player.charging_shot:
            power_width = 50
            power_height = 8
            power_x = pos_2d[0] - power_width // 2
            power_y = pos_2d[1] + 30
            
            # Background
            self.canvas.create_rectangle(
                power_x, power_y, power_x + power_width, power_y + power_height,
                fill="gray", outline="black", width=1
            )
            
            # Power fill with pulsing effect
            power_fill = (player.shot_power / 100.0) * power_width
            power_intensity = 0.5 + 0.5 * math.sin(time.time() * 10)
            
            if player.shot_power < 30:
                power_color = "yellow"
            elif player.shot_power < 70:
                power_color = "orange"  
            else:
                power_color = "red"
            
            self.canvas.create_rectangle(
                power_x, power_y, power_x + power_fill, power_y + power_height,
                fill=power_color, outline=""
            )
            
            # Power percentage text
            self.canvas.create_text(
                pos_2d[0], power_y + power_height + 15,
                text=f"{int(player.shot_power)}%",
                fill="white", font=("Arial", 10, "bold")
            )
        
        # Momentum indicator
        if abs(player.momentum) > 20:
            momentum_text = "🔥" if player.momentum > 50 else "📈" if player.momentum > 0 else "📉"
            self.canvas.create_text(
                pos_2d[0] + 25, pos_2d[1] - 45,
                text=momentum_text, font=("Arial", 16)
            )
    
    def draw_hit_effect(self, player: Player, pos_2d: Tuple[float, float]):
        """Draw hit impact effects"""
        effect_alpha = player.hit_effect_time / 0.3
        effect_size = (1.0 - effect_alpha) * 30 + 10
        
        # Impact burst
        burst_color = "yellow" if player.selected_shot_type == ShotType.SMASH else "lightblue"
        for i in range(8):
            angle = i * (2 * math.pi / 8)
            line_end_x = pos_2d[0] + math.cos(angle) * effect_size
            line_end_y = pos_2d[1] + math.sin(angle) * effect_size
            
            self.canvas.create_line(
                pos_2d[0], pos_2d[1], line_end_x, line_end_y,
                fill=burst_color, width=3
            )
    
    def draw_shuttlecock_detailed(self, shuttlecock: Shuttlecock, particle_system: ParticleSystem):
        """Draw detailed shuttlecock with trails and effects"""
        # Draw trail
        if self.show_trails and len(shuttlecock.trail_positions) > 1:
            self.draw_shuttlecock_trail(shuttlecock)
        
        # Draw shadow on ground
        self.draw_shuttlecock_shadow(shuttlecock)
        
        # Draw main shuttlecock body
        pos_2d = self.project_3d_to_2d(shuttlecock.position)
        
        # Cork part (main body)
        cork_size = SHUTTLECOCK_SIZE
        speed_factor = min(2.0, shuttlecock.get_current_speed() / 200.0)
        cork_size = int(cork_size * (1 + speed_factor * 0.5))
        
        self.canvas.create_oval(
            pos_2d[0] - cork_size, pos_2d[1] - cork_size,
            pos_2d[0] + cork_size, pos_2d[1] + cork_size,
            fill="white", outline="black", width=2
        )
        
        # Draw feathers with rotation
        self.draw_shuttlecock_feathers(shuttlecock, pos_2d)
        
        # Height indicator
        if shuttlecock.position.z > 10:
            self.draw_height_indicator(shuttlecock, pos_2d)
        
        # Speed indicator
        if self.show_stats:
            self.draw_speed_indicator(shuttlecock, pos_2d)
        
        # Draw particles if available
        if self.render_particles:
            for particle in particle_system.particles:
                self.draw_particle(particle)
    
    def draw_shuttlecock_trail(self, shuttlecock: Shuttlecock):
        """Draw shuttlecock movement trail"""
        if len(shuttlecock.trail_positions) < 2:
            return
        
        for i in range(1, len(shuttlecock.trail_positions)):
            alpha = i / len(shuttlecock.trail_positions)
            trail_pos_1 = self.project_3d_to_2d(shuttlecock.trail_positions[i-1])
            trail_pos_2 = self.project_3d_to_2d(shuttlecock.trail_positions[i])
            
            # Color based on speed
            speed = (shuttlecock.trail_positions[i] - shuttlecock.trail_positions[i-1]).length() * 60
            if speed > 200:
                trail_color = "red"
            elif speed > 100:
                trail_color = "orange"  
            else:
                trail_color = "lightblue"
            
            trail_width = int(1 + alpha * 3)
            
            self.canvas.create_line(
                trail_pos_1[0], trail_pos_1[1], trail_pos_2[0], trail_pos_2[1],
                fill=trail_color, width=trail_width
            )
    
    def draw_shuttlecock_shadow(self, shuttlecock: Shuttlecock):
        """Draw shuttlecock shadow on ground"""
        shadow_pos = self.project_3d_to_2d(Vector3D(shuttlecock.position.x, shuttlecock.position.y, 0))
        shadow_size = max(3, 12 - (shuttlecock.position.z / 20))
        shadow_alpha = max(0.1, 1.0 - shuttlecock.position.z / 150.0)
        
        # Multiple shadow circles for blur effect
        for i in range(3):
            size = shadow_size + i * 2
            gray_value = int(30 + i * 20)
            shadow_color = f"#{gray_value:02x}{gray_value:02x}{gray_value:02x}"
            
            self.canvas.create_oval(
                shadow_pos[0] - size, shadow_pos[1] - size,
                shadow_pos[0] + size, shadow_pos[1] + size,
                fill=shadow_color, outline=""
            )
    
    def draw_shuttlecock_feathers(self, shuttlecock: Shuttlecock, pos_2d: Tuple[float, float]):
        """Draw animated feathers"""
        feather_count = 16
        base_length = SHUTTLECOCK_SIZE * 2
        
        for i in range(feather_count):
            angle = (i * 360 / feather_count + shuttlecock.spin) % 360
            angle_rad = math.radians(angle)
            
            # Feather length varies with spin and speed
            speed_factor = shuttlecock.get_current_speed() / 300.0
            feather_length = base_length * (1 + speed_factor * 0.3)
            
            # Feather position
            feather_x = pos_2d[0] + math.cos(angle_rad) * feather_length
            feather_y = pos_2d[1] + math.sin(angle_rad) * feather_length
            
            # Feather color alternation
            feather_color = "white" if i % 2 == 0 else "lightgray"
            feather_width = 2 if i % 4 == 0 else 1
            
            self.canvas.create_line(
                pos_2d[0], pos_2d[1], feather_x, feather_y,
                fill=feather_color, width=feather_width
            )
    
    def draw_height_indicator(self, shuttlecock: Shuttlecock, pos_2d: Tuple[float, float]):
        """Draw height indicator line and text"""
        ground_pos = self.project_3d_to_2d(Vector3D(shuttlecock.position.x, shuttlecock.position.y, 0))
        
        # Height line
        self.canvas.create_line(
            ground_pos[0], ground_pos[1], pos_2d[0], pos_2d[1],
            fill="cyan", width=1, dash=(3, 3)
        )
        
        # Height text
        height_text = f"{int(shuttlecock.position.z)}m"
        self.canvas.create_text(
            pos_2d[0] + 20, pos_2d[1] - 15,
            text=height_text, fill="cyan", 
            font=("Arial", 9, "bold")
        )
    
    def draw_speed_indicator(self, shuttlecock: Shuttlecock, pos_2d: Tuple[float, float]):
        """Draw speed indicator"""
        current_speed = shuttlecock.get_current_speed()
        speed_kmh = int(current_speed * 3.6)  # Convert to km/h
        
        # Speed text with color coding
        if speed_kmh > 300:
            speed_color = "red"
        elif speed_kmh > 200:
            speed_color = "orange"
        elif speed_kmh > 100:
            speed_color = "yellow"
        else:
            speed_color = "white"
        
        self.canvas.create_text(
            pos_2d[0] - 20, pos_2d[1] - 15,
            text=f"{speed_kmh}km/h", fill=speed_color,
            font=("Arial", 8)
        )
    
    def draw_particle(self, particle: Particle):
        """Draw individual particle"""
        pos_2d = self.project_3d_to_2d(particle.position)
        alpha = particle.get_alpha()
        size = particle.size * alpha
        
        if size > 0.5:
            self.canvas.create_oval(
                pos_2d[0] - size, pos_2d[1] - size,
                pos_2d[0] + size, pos_2d[1] + size,
                fill=particle.color, outline=""
            )
    
    def draw_ui_overlay(self, game):
        """Draw comprehensive UI overlay"""
        # Score board
        self.draw_scoreboard(game)
        
        # Game statistics
        if self.show_stats:
            self.draw_game_statistics(game)
        
        # Controls help
        self.draw_controls_help()
        
        # Match information
        self.draw_match_info(game)
        
        # Rally information
        if hasattr(game, 'rally_count') and game.rally_count > 0:
            self.draw_rally_info(game)
    
    def draw_scoreboard(self, game):
        """Draw main scoreboard"""
        # Background
        self.canvas.create_rectangle(10, 10, 350, 120, 
                                   fill="black", outline="white", width=3)
        
        # Scores
        score_text = f"{game.player1.stats.name}: {game.score[0]}  |  {game.player2.stats.name}: {game.score[1]}"
        self.canvas.create_text(180, 35, text=score_text, fill="white", 
                              font=("Arial", 16, "bold"))
        
        # Set information
        set_text = f"Set {game.current_set} of {game.max_sets}"
        self.canvas.create_text(180, 55, text=set_text, fill="yellow", 
                              font=("Arial", 12))
        
        # Serving player
        serving_text = f"Serving: {game.serving_player.stats.name}"
        self.canvas.create_text(180, 75, text=serving_text, fill="lightgreen", 
                              font=("Arial", 10))
        
        # Game mode
        mode_text = f"Rally: {getattr(game, 'rally_count', 0)}"
        self.canvas.create_text(180, 95, text=mode_text, fill="lightgray", 
                              font=("Arial", 10))
    
    def draw_game_statistics(self, game):
        """Draw detailed game statistics"""
        stats_x = WINDOW_WIDTH - 280
        stats_y = 10
        stats_width = 270
        stats_height = 200
        
        # Background
        self.canvas.create_rectangle(stats_x, stats_y, stats_x + stats_width, stats_y + stats_height,
                                   fill="black", outline="white", width=2)
        
        # Title
        self.canvas.create_text(stats_x + stats_width//2, stats_y + 15,
                              text="Match Statistics", fill="yellow",
                              font=("Arial", 12, "bold"))
        
        # Statistics data
        stats_data = [
            f"Total Rallies: {getattr(game, 'total_rallies', 0)}",
            f"Longest Rally: {getattr(game, 'longest_rally', 0)}",
            f"Match Duration: {self.format_time(getattr(game, 'match_duration', 0))}",
            f"",
            f"{game.player1.stats.name} Stats:",
            f"  Shots: {game.player1.stats.total_shots}",
            f"  Smashes: {game.player1.stats.total_smashes}",
            f"  Stamina: {int(game.player1.stats.stamina)}%",
            f"",
            f"{game.player2.stats.name} Stats:",
            f"  Shots: {game.player2.stats.total_shots}",
            f"  Smashes: {game.player2.stats.total_smashes}",
            f"  Stamina: {int(game.player2.stats.stamina)}%"
        ]
        
        for i, stat in enumerate(stats_data):
            if stat:  # Skip empty lines
                self.canvas.create_text(stats_x + 10, stats_y + 35 + i * 12,
                                      anchor="w", text=stat, fill="white",
                                      font=("Arial", 9))
    
    def draw_controls_help(self):
        """Draw controls help"""
        help_y = WINDOW_HEIGHT - 150
        controls = [
            "WASD: Move Player",
            "SPACE: Charge Shot", 
            "1: Clear  2: Drop  3: Drive  4: Smash",
            "5: Lift  6: Net Shot",
            "P: Pause  R: Reset  C: Camera  T: Toggle Trails"
        ]
        
        for i, control in enumerate(controls):
            self.canvas.create_text(10, help_y + i * 15, anchor="w", text=control,
                                  fill="lightgray", font=("Arial", 10))
    
    def draw_match_info(self, game):
        """Draw match information"""
        info_x = 10
        info_y = WINDOW_HEIGHT - 200
        
        # Weather and conditions
        weather_text = f"Weather: {getattr(game, 'weather', 'Perfect')}"
        self.canvas.create_text(info_x, info_y, anchor="w", text=weather_text,
                              fill="lightblue", font=("Arial", 10))
        
        # Court information
        court_text = "Court: Indoor Championship Court"
        self.canvas.create_text(info_x, info_y + 15, anchor="w", text=court_text,
                              fill="lightblue", font=("Arial", 10))
    
    def draw_rally_info(self, game):
        """Draw current rally information"""
        rally_x = WINDOW_WIDTH // 2
        rally_y = 50
        
        rally_text = f"Rally {game.rally_count}"
        if game.rally_count > 10:
            rally_text += " - Long Rally!"
            text_color = "orange"
        elif game.rally_count > 20:
            rally_text += " - Epic Rally!"
            text_color = "red"
        else:
            text_color = "white"
        
        self.canvas.create_text(rally_x, rally_y, text=rally_text,
                              fill=text_color, font=("Arial", 14, "bold"))
    
    def format_time(self, seconds: float) -> str:
        """Format time in minutes:seconds"""
        minutes = int(seconds // 60)
        seconds = int(seconds % 60)
        return f"{minutes:02d}:{seconds:02d}"
    
    def update_camera(self, target_pos: Vector3D = None):
        """Update camera position for cinematic effects"""
        if target_pos:
            # Smooth camera follow
            camera_target = Vector3D(target_pos.x, target_pos.y - 50, 100)
            lerp_factor = 0.05
            self.camera_position = self.camera_position.lerp(camera_target, lerp_factor)
    
    def add_screen_shake(self, intensity: float):
        """Add screen shake effect"""
        self.screen_shake = min(10, intensity)
    
    def add_flash_effect(self, intensity: float = 0.3):
        """Add flash effect"""
        self.flash_effect = min(1.0, intensity)

class SoundManager:
    def __init__(self):
        self.enabled = True
        self.volume = 0.7
        self.sound_queue = []
        
        # Sound effect descriptions (would be actual audio in full implementation)
        self.sound_effects = {
            'hit_shuttlecock': "Racket impact sound",
            'shuttlecock_land': "Shuttlecock hitting ground", 
            'game_point': "Point scored fanfare",
            'game_over': "Match finished sound",
            'serve': "Service sound",
            'net_hit': "Net collision sound",
            'smash': "Powerful smash sound",
            'applause': "Crowd applause",
            'whistle': "Referee whistle"
        }
    
    def play_sound(self, sound_name: str, volume: float = 1.0):
        """Play sound effect"""
        if not self.enabled:
            return
        
        # In a real implementation, this would trigger actual audio playback
        print(f"🔊 {self.sound_effects.get(sound_name, 'Unknown sound')}")
    
    def play_commentary(self, text: str):
        """Play commentary text"""
        if self.enabled:
            print(f"🎤 Commentary: {text}")

class GameLogic:
    def __init__(self):
        self.court = Court()
        self.player1 = None
        self.player2 = None
        self.shuttlecock = None
        self.current_player = None
        self.serving_player = None
        self.receiving_player = None
        
        # Game state
        self.game_state = GameState.MENU
        self.score = [0, 0]  # [player1_score, player2_score]
        self.sets_won = [0, 0]  # [player1_sets, player2_sets]
        self.current_set = 1
        self.max_sets = 3
        self.points_to_win_set = 21
        self.min_point_difference = 2
        
        # Rally tracking
        self.rally_count = 0
        self.total_rallies = 0
        self.longest_rally = 0
        self.current_rally_shots = 0
        self.last_shot_player = None
        
        # Serve tracking
        self.serve_count = 0
        self.service_side = "right"  # right or left
        self.consecutive_serves = 0
        
        # Match tracking
        self.match_start_time = 0
        self.match_duration = 0
        self.match_stats = MatchStats()
        self.weather = WeatherCondition.PERFECT
        
        # AI and difficulty
        self.ai_players = {}
        
        # Game events
        self.recent_events = []
        self.commentary_system = None
        
    def initialize_match(self, player1_name: str, player1_type: PlayerType,
                        player2_name: str, player2_type: PlayerType):
        """Initialize a new match"""
        # Create players
        self.player1 = Player(player1_name, COURT_WIDTH//2, COURT_HEIGHT*0.2, player1_type)
        self.player2 = Player(player2_name, COURT_WIDTH//2, COURT_HEIGHT*0.8, player2_type)
        
        # Set up AI players
        if player1_type != PlayerType.HUMAN:
            difficulty = player1_type.value.replace('ai_', '')
            self.ai_players[self.player1] = AI(self.player1, difficulty)
        
        if player2_type != PlayerType.HUMAN:
            difficulty = player2_type.value.replace('ai_', '')
            self.ai_players[self.player2] = AI(self.player2, difficulty)
        
        # Initialize game state
        self.serving_player = self.player1
        self.receiving_player = self.player2
        self.current_player = self.serving_player
        
        # Create shuttlecock
        self.shuttlecock = Shuttlecock(COURT_WIDTH//2, COURT_HEIGHT*0.25, 30)
        
        # Reset scores and stats
        self.reset_match_stats()
        
        # Set random weather
        self.weather = random.choice(list(WeatherCondition))
        
        self.game_state = GameState.SERVING
        self.match_start_time = time.time()
        
        print(f"Match initialized: {player1_name} vs {player2_name}")
        print(f"Weather conditions: {self.weather.value}")
    
    def reset_match_stats(self):
        """Reset all match statistics"""
        self.score = [0, 0]
        self.sets_won = [0, 0]
        self.current_set = 1
        self.rally_count = 0
        self.total_rallies = 0
        self.longest_rally = 0
        self.current_rally_shots = 0
        self.serve_count = 0
        self.consecutive_serves = 0
        self.match_stats = MatchStats()
        self.recent_events.clear()
    
    def update(self, dt: float):
        """Main game update loop"""
        if self.game_state == GameState.MENU:
            return
        
        # Update match duration
        if self.match_start_time > 0:
            self.match_duration = time.time() - self.match_start_time
        
        # Update players
        if self.player1:
            self.player1.update(dt, self)
        if self.player2:
            self.player2.update(dt, self)
        
        # Update AI players
        for player, ai in self.ai_players.items():
            ai.update(self, dt)
        
        # Update shuttlecock
        if self.shuttlecock:
            self.shuttlecock.update(dt, self.weather)
            
            # Check for shuttlecock events
            self.check_shuttlecock_events()
        
        # Update game state
        self.update_game_state()
        
        # Check for game end conditions
        self.check_end_conditions()
    
    def check_shuttlecock_events(self):
        """Check for shuttlecock-related events"""
        if not self.shuttlecock or not self.shuttlecock.is_in_play:
            return
        
        # Check if shuttlecock hit the ground
        if self.shuttlecock.position.z <= 0 and self.shuttlecock.velocity.length() < 5:
            self.handle_shuttlecock_landing()
        
        # Check if shuttlecock hit the net
        if self.court.is_net_hit(self.shuttlecock.position):
            self.handle_net_hit()
        
        # Check if shuttlecock went out of bounds
        if not self.court.is_in_bounds(self.shuttlecock.position.x, self.shuttlecock.position.y):
            self.handle_out_of_bounds()
        
        # Check if shuttlecock is too high (unrealistic)
        if self.shuttlecock.position.z > 300:
            self.shuttlecock.position.z = 300
            self.shuttlecock.velocity.z = min(0, self.shuttlecock.velocity.z)
    
    def handle_shuttlecock_landing(self):
        """Handle shuttlecock landing on court"""
        if not self.shuttlecock.is_in_play:
            return
        
        self.shuttlecock.is_in_play = False
        landing_pos = Vector3D(self.shuttlecock.position.x, self.shuttlecock.position.y, 0)
        
        # Determine which side it landed on
        landing_side = self.court.get_court_side(landing_pos.y)
        
        # Award point based on game state and landing position
        if self.game_state == GameState.SERVING:
            # Check if serve was valid
            if self.is_valid_serve(landing_pos):
                self.start_rally()
                return
            else:
                # Service fault
                self.handle_service_fault()
                return
        
        # Regular rally - point goes to opponent of the side where it landed
        if landing_side == self.player1.current_side:
            # Landed on player1's side, point to player2
            self.award_point(self.player2)
        else:
            # Landed on player2's side, point to player1
            self.award_point(self.player1)
        
        self.add_event("shuttlecock_landing", f"Shuttlecock landed at {int(landing_pos.x)}, {int(landing_pos.y)}")
    
    def handle_net_hit(self):
        """Handle shuttlecock hitting the net"""
        if not self.shuttlecock.is_in_play:
            return
        
        self.shuttlecock.is_in_play = False
        
        # Award point to opponent of last player who hit
        if self.shuttlecock.last_player_hit == self.player1:
            self.award_point(self.player2)
        elif self.shuttlecock.last_player_hit == self.player2:
            self.award_point(self.player1)
        
        self.add_event("net_hit", "Shuttlecock hit the net!")
    
    def handle_out_of_bounds(self):
        """Handle shuttlecock going out of bounds"""
        if not self.shuttlecock.is_in_play:
            return
        
        self.shuttlecock.is_in_play = False
        
        # Award point to opponent of last player who hit
        if self.shuttlecock.last_player_hit == self.player1:
            self.award_point(self.player2)
        elif self.shuttlecock.last_player_hit == self.player2:
            self.award_point(self.player1)
        
        self.add_event("out_of_bounds", "Shuttlecock went out of bounds!")
    
    def handle_service_fault(self):
        """Handle service fault"""
        # Service fault - point to receiving player
        self.award_point(self.receiving_player)
        self.add_event("service_fault", f"Service fault by {self.serving_player.stats.name}")
    
    def is_valid_serve(self, landing_pos: Vector3D) -> bool:
        """Check if serve is valid"""
        serving_side = self.serving_player.current_side
        return self.court.is_in_service_area(landing_pos.x, landing_pos.y, serving_side)
    
    def start_rally(self):
        """Start a rally after successful serve"""
        self.game_state = GameState.RALLY
        self.rally_count = 1
        self.current_rally_shots = 0
        self.shuttlecock.is_in_play = True
        
        self.add_event("rally_start", "Rally started!")
    
    def award_point(self, player: Player):
        """Award a point to a player"""
        if player == self.player1:
            self.score[0] += 1
        else:
            self.score[1] += 1
        
        player.stats.points_scored += 1
        player.celebrate()
        
        # Update rally stats
        if self.rally_count > self.longest_rally:
            self.longest_rally = self.rally_count
        
        if self.rally_count > 0:
            self.total_rallies += 1
            self.match_stats.total_rallies += 1
            
            if self.rally_count < self.match_stats.shortest_rally:
                self.match_stats.shortest_rally = self.rally_count
        
        # Reset for next serve
        self.rally_count = 0
        self.current_rally_shots = 0
        
        # Switch server if necessary
        self.update_serving_player()
        
        # Check for set/match win
        if self.check_set_win():
            self.handle_set_win(player)
        else:
            # Prepare for next serve
            self.prepare_next_serve()
        
        self.add_event("point_awarded", f"Point to {player.stats.name}! Score: {self.score[0]}-{self.score[1]}")
    
    def update_serving_player(self):
        """Update who is serving based on scoring rules"""
        # In badminton, server changes when receiving side wins a rally
        if self.score[0] + self.score[1] > 0:  # Not the first point
            if ((self.serving_player == self.player1 and self.score[1] > self.score[0]) or 
                (self.serving_player == self.player2 and self.score[0] > self.score[1])):
                # Switch server
                if self.serving_player == self.player1:
                    self.serving_player = self.player2
                    self.receiving_player = self.player1
                else:
                    self.serving_player = self.player1
                    self.receiving_player = self.player2
        
        self.consecutive_serves = 0
    
    def check_set_win(self) -> bool:
        """Check if current set is won"""
        max_score = max(self.score)
        min_score = min(self.score)
        
        # Must reach minimum points and have minimum difference
        return (max_score >= self.points_to_win_set and 
                (max_score - min_score) >= self.min_point_difference)
    
    def handle_set_win(self, winner: Player):
        """Handle set victory"""
        if winner == self.player1:
            self.sets_won[0] += 1
        else:
            self.sets_won[1] += 1
        
        winner.stats.sets_won += 1
        loser = self.player2 if winner == self.player1 else self.player1
        loser.stats.sets_lost += 1
        
        self.add_event("set_won", f"{winner.stats.name} wins set {self.current_set}!")
        
        # Check for match win
        if self.sets_won[0] > self.max_sets // 2 or self.sets_won[1] > self.max_sets // 2:
            self.handle_match_win(winner)
        else:
            # Start next set
            self.current_set += 1
            self.score = [0, 0]
            self.prepare_next_serve()
    
    def handle_match_win(self, winner: Player):
        """Handle match victory"""
        self.game_state = GameState.MATCH_WON
        
        winner.stats.wins += 1
        winner.stats.update_experience(100)
        
        loser = self.player2 if winner == self.player1 else self.player1
        loser.stats.losses += 1
        loser.stats.update_experience(25)
        
        # Final match statistics
        self.match_stats.duration = self.match_duration
        if self.total_rallies > 0:
            self.match_stats.average_rally_length = self.current_rally_shots / self.total_rallies
        
        self.add_event("match_won", f"{winner.stats.name} wins the match!")
        print(f"🏆 {winner.stats.name} wins the match {self.sets_won[0]}-{self.sets_won[1]}!")
    
    def prepare_next_serve(self):
        """Prepare for next serve"""
        self.game_state = GameState.SERVING
        self.current_player = self.serving_player
        
        # Position shuttlecock for serve
        if self.serving_player.current_side == "near":
            serve_x = COURT_WIDTH // 2
            serve_y = COURT_HEIGHT * 0.25
        else:
            serve_x = COURT_WIDTH // 2
            serve_y = COURT_HEIGHT * 0.75
        
        self.shuttlecock = Shuttlecock(serve_x, serve_y, 20)
        self.shuttlecock.is_in_play = False
        
        # Position players for serve
        self.serving_player.move_to(serve_x, serve_y)
        if self.receiving_player.current_side == "near":
            self.receiving_player.move_to(COURT_WIDTH // 2, COURT_HEIGHT * 0.25)
        else:
            self.receiving_player.move_to(COURT_WIDTH // 2, COURT_HEIGHT * 0.75)
    
    def execute_serve(self):
        """Execute a serve"""
        if self.game_state != GameState.SERVING or not self.serving_player.ready_to_hit:
            return False
        
        # Calculate serve target
        if self.serving_player.current_side == "near":
            target_y = COURT_HEIGHT * 0.7
        else:
            target_y = COURT_HEIGHT * 0.3
        
        target_pos = Vector3D(
            COURT_WIDTH // 2 + random.uniform(-50, 50),
            target_y + random.uniform(-20, 20),
            0
        )
        
        # Execute serve
        shot_info = self.serving_player.release_shot(self.shuttlecock, target_pos)
        if shot_info:
            direction = shot_info['direction'].normalize()
            self.shuttlecock.hit(self.serving_player, ShotType.SERVE, 
                               shot_info['power'], direction)
            
            self.serve_count += 1
            self.consecutive_serves += 1
            
            self.add_event("serve_executed", f"Serve by {self.serving_player.stats.name}")
            return True
        
        return False
    
    def try_hit_shuttlecock(self, player: Player, shot_type: ShotType = None) -> bool:
        """Try to hit shuttlecock with player"""
        if not self.shuttlecock or not self.shuttlecock.is_in_play:
            return False
        
        # Check if player can reach shuttlecock
        if not player.can_reach_shuttlecock(self.shuttlecock):
            return False
        
        # Use selected shot type or default
        if shot_type is None:
            shot_type = player.selected_shot_type
        
        # Calculate target position based on strategy
        opponent = self.player2 if player == self.player1 else self.player1
        target_pos = self.calculate_shot_target(player, opponent, shot_type)
        
        # Execute shot
        shot_info = player.release_shot(self.shuttlecock, target_pos)
        if shot_info:
            success_roll = random.random()
            
            if success_roll < shot_info['success_chance']:
                # Successful shot
                direction = shot_info['direction'].normalize()
                self.shuttlecock.hit(player, shot_type, shot_info['power'], direction)
                
                player.stats.successful_shots += 1
                if shot_type == ShotType.SMASH:
                    player.stats.successful_smashes += 1
                
                self.current_rally_shots += 1
                self.rally_count = max(1, self.rally_count + 1)
                
                # Switch current player
                self.current_player = opponent
                
                self.add_event("shot_success", f"{player.stats.name} hits {shot_type.value}!")
                return True
            else:
                # Failed shot
                player.stats.unforced_errors += 1
                player.show_frustration()
                self.award_point(opponent)
                
                self.add_event("shot_failed", f"{player.stats.name} mishits!")
                return False
        
        return False
    
    def calculate_shot_target(self, player: Player, opponent: Player, shot_type: ShotType) -> Vector3D:
        """Calculate optimal target for shot"""
        # Base target on opposite side
        if player.current_side == "near":
            base_y = COURT_HEIGHT * 0.8
        else:
            base_y = COURT_HEIGHT * 0.2
        
        target = Vector3D(COURT_WIDTH // 2, base_y, 0)
        
        # Adjust based on shot type
        if shot_type == ShotType.SMASH:
            # Aim for corners, away from opponent
            if opponent.position.x < COURT_WIDTH // 2:
                target.x = COURT_WIDTH * 0.8
            else:
                target.x = COURT_WIDTH * 0.2
        elif shot_type == ShotType.DROP:
            # Aim for net area
            target.y = COURT_HEIGHT // 2 + (30 if player.current_side == "near" else -30)
        elif shot_type == ShotType.CLEAR:
            # Aim for back court
            target.y = base_y
        
        # Add some randomness
        target.x += random.uniform(-30, 30)
        target.y += random.uniform(-20, 20)
        
        # Keep in bounds
        target.x = max(20, min(COURT_WIDTH - 20, target.x))
        target.y = max(20, min(COURT_HEIGHT - 20, target.y))
        
        return target
    
    def update_game_state(self):
        """Update overall game state"""
        if self.game_state == GameState.SERVING:
            # Auto-serve for AI players after delay
            if (self.serving_player in self.ai_players and 
                time.time() - self.match_start_time > 1.0):
                self.execute_serve()
        
        elif self.game_state == GameState.RALLY:
            # Check for rally timeout (shuttlecock stopped moving)
            if (self.shuttlecock and 
                self.shuttlecock.velocity.length() < 5 and 
                self.shuttlecock.position.z <= 5):
                # Rally ended due to inactivity
                if self.shuttlecock.last_player_hit:
                    opponent = (self.player2 if self.shuttlecock.last_player_hit == self.player1 
                              else self.player1)
                    self.award_point(opponent)
    
    def check_end_conditions(self):
        """Check for various end conditions"""
        # Check for player stamina depletion
        if self.player1.stats.stamina <= 0:
            self.player1.stats.stamina = 1
            self.player1.show_frustration()
        
        if self.player2.stats.stamina <= 0:
            self.player2.stats.stamina = 1
            self.player2.show_frustration()
        
        # Check for match timeout (very long matches)
        if self.match_duration > 3600:  # 1 hour
            self.add_event("match_timeout", "Match timed out due to length")
    
    def add_event(self, event_type: str, description: str):
        """Add event to recent events list"""
        event = {
            'type': event_type,
            'description': description,
            'timestamp': time.time(),
            'match_time': self.match_duration
        }
        
        self.recent_events.append(event)
        
        # Keep only recent events
        if len(self.recent_events) > 50:
            self.recent_events.pop(0)
        
        # Print important events
        if event_type in ['point_awarded', 'set_won', 'match_won', 'rally_start']:
            print(f"📊 {description}")
    
    def pause_game(self):
        """Pause the game"""
        if self.game_state == GameState.PLAYING:
            self.game_state = GameState.PAUSED
    
    def resume_game(self):
        """Resume the game"""
        if self.game_state == GameState.PAUSED:
            self.game_state = GameState.PLAYING
    
    def reset_game(self):
        """Reset the game"""
        self.reset_match_stats()
        if self.player1 and self.player2:
            self.initialize_match(
                self.player1.stats.name, self.player1.player_type,
                self.player2.stats.name, self.player2.player_type
            )

class BadmintonGame:
    def __init__(self):
        print("Initializing Badminton Game...")
        
        self.root = tk.Tk()
        self.root.title("3D Badminton Championship")
        self.root.geometry(f"{WINDOW_WIDTH}x{WINDOW_HEIGHT}")
        self.root.configure(bg="black")
        self.root.resizable(False, False)
        
        # Make sure window is on top and focused
        self.root.lift()
        self.root.attributes('-topmost', True)
        self.root.after_idle(lambda: self.root.attributes('-topmost', False))
        
        # Main canvas
        self.canvas = tk.Canvas(
            self.root, width=WINDOW_WIDTH, height=WINDOW_HEIGHT,
            bg="black", highlightthickness=0
        )
        self.canvas.pack()
        
        # Game systems
        print("Initializing game systems...")
        self.game_logic = GameLogic()
        self.renderer = GameRenderer(self.canvas)
        self.particle_system = ParticleSystem()
        self.sound_manager = SoundManager()
        
        # Input handling
        self.keys_pressed = set()
        
        # Game loop
        self.is_running = False
        self.last_update_time = time.time()
        
        print("Game systems initialized!")
        print("Showing main menu...")
        
        # Show menu after short delay to ensure window is ready
        self.root.after(100, self.show_main_menu)
    
    def setup_input_handling(self):
        """Setup keyboard input handling"""
        self.root.bind('<KeyPress>', self.on_key_press)
        self.root.bind('<KeyRelease>', self.on_key_release)
        self.root.focus_set()
        
        # Mouse handling
        self.canvas.bind('<Button-1>', self.on_mouse_click)
        self.canvas.bind('<Motion>', self.on_mouse_move)
    
    def on_key_press(self, event):
        """Handle key press events"""
        key = event.keysym.lower()
        self.keys_pressed.add(key)
        
        # Game controls
        if key == 'p':
            self.toggle_pause()
        elif key == 'r':
            self.reset_game()
        elif key == 'c':
            self.cycle_camera()
        elif key == 't':
            self.renderer.show_trails = not self.renderer.show_trails
        elif key == 'h':
            self.renderer.show_stats = not self.renderer.show_stats
        elif key == 'escape':
            self.show_main_menu()
        
        # Shot type selection
        shot_keys = {
            '1': ShotType.CLEAR,
            '2': ShotType.DROP, 
            '3': ShotType.DRIVE,
            '4': ShotType.SMASH,
            '5': ShotType.LIFT,
            '6': ShotType.NET_SHOT
        }
        
        if key in shot_keys and self.game_logic.player1:
            self.game_logic.player1.selected_shot_type = shot_keys[key]
        
        # Human player controls (Player 1)
        if self.game_logic.game_state in [GameState.SERVING, GameState.RALLY]:
            if key == 'space':
                if self.game_logic.game_state == GameState.SERVING:
                    if self.game_logic.serving_player == self.game_logic.player1:
                        self.game_logic.execute_serve()
                else:
                    self.game_logic.player1.start_charging_shot()
    
    def on_key_release(self, event):
        """Handle key release events"""
        key = event.keysym.lower()
        self.keys_pressed.discard(key)
        
        # Release shot when space is released
        if key == 'space' and self.game_logic.player1:
            if self.game_logic.player1.charging_shot:
                self.game_logic.try_hit_shuttlecock(self.game_logic.player1)
    
    def on_mouse_click(self, event):
        """Handle mouse click events"""
        if self.game_logic.game_state == GameState.MENU:
            # Handle menu clicks
            pass
        else:
            # In-game clicks
            pass
    
    def on_mouse_move(self, event):
        """Handle mouse movement"""
        # Could be used for camera control
        pass
    
    def handle_movement_input(self, dt: float):
        """Handle continuous movement input"""
        if not self.game_logic.player1 or self.game_logic.player1.player_type != PlayerType.HUMAN:
            return
        
        movement_speed = 200 * dt
        dx, dy = 0, 0
        
        if 'w' in self.keys_pressed or 'up' in self.keys_pressed:
            dy = -movement_speed
        if 's' in self.keys_pressed or 'down' in self.keys_pressed:
            dy = movement_speed
        if 'a' in self.keys_pressed or 'left' in self.keys_pressed:
            dx = -movement_speed
        if 'd' in self.keys_pressed or 'right' in self.keys_pressed:
            dx = movement_speed
        
        if dx != 0 or dy != 0:
            self.game_logic.player1.move_relative(dx, dy)
    
    def show_main_menu(self):
        """Show main menu"""
        self.game_logic.game_state = GameState.MENU
        self.is_running = False
        
        # Clear canvas
        self.canvas.delete("all")
        
        # Draw menu background
        self.renderer.draw_background()
        
        # Menu title
        self.canvas.create_text(
            WINDOW_WIDTH // 2, 100,
            text="🏸 3D BADMINTON CHAMPIONSHIP 🏸",
            fill="gold", font=("Arial", 24, "bold")
        )
        
        # Menu options with clickable buttons
        menu_y_start = 250
        menu_spacing = 60
        
        # Create clickable menu buttons
        self.create_menu_button("1. Quick Match (vs AI)", menu_y_start, self.start_quick_match)
        self.create_menu_button("2. Tournament Mode", menu_y_start + menu_spacing, self.start_tournament)
        self.create_menu_button("3. Training Mode", menu_y_start + menu_spacing * 2, self.start_training)
        self.create_menu_button("4. Settings", menu_y_start + menu_spacing * 3, self.show_settings)
        self.create_menu_button("5. Exit", menu_y_start + menu_spacing * 4, self.exit_game)
        
        # Instructions
        self.canvas.create_text(
            WINDOW_WIDTH // 2, 600,
            text="Click on options above or press number keys",
            fill="yellow", font=("Arial", 14, "bold")
        )
        
        instructions = [
            "Game Controls:",
            "WASD: Move player",
            "SPACE: Charge/Release shot",
            "1-6: Select shot type",
            "P: Pause, R: Reset, C: Camera, T: Toggle trails"
        ]
        
        for i, instruction in enumerate(instructions):
            self.canvas.create_text(
                WINDOW_WIDTH // 2, 650 + i * 20,
                text=instruction, fill="lightgray",
                font=("Arial", 10)
            )
        
        # Rebind key events for menu
        self.root.unbind('<KeyPress>')
        self.root.bind('<KeyPress>', self.handle_menu_keys)
        
        # Focus on root to ensure key events work
        self.root.focus_set()
    
    def create_menu_button(self, text: str, y_pos: int, command):
        """Create a clickable menu button"""
        button_width = 400
        button_height = 40
        button_x = WINDOW_WIDTH // 2 - button_width // 2
        
        # Button background
        button_rect = self.canvas.create_rectangle(
            button_x, y_pos - button_height // 2,
            button_x + button_width, y_pos + button_height // 2,
            fill="darkblue", outline="white", width=2
        )
        
        # Button text
        button_text = self.canvas.create_text(
            WINDOW_WIDTH // 2, y_pos,
            text=text, fill="white",
            font=("Arial", 16, "bold")
        )
        
        # Store button info for click detection
        self.canvas.tag_bind(button_rect, '<Button-1>', lambda e: command())
        self.canvas.tag_bind(button_text, '<Button-1>', lambda e: command())
        
        # Hover effects
        def on_enter(event):
            self.canvas.itemconfig(button_rect, fill="blue")
            self.canvas.itemconfig(button_text, fill="yellow")
        
        def on_leave(event):
            self.canvas.itemconfig(button_rect, fill="darkblue") 
            self.canvas.itemconfig(button_text, fill="white")
        
        self.canvas.tag_bind(button_rect, '<Enter>', on_enter)
        self.canvas.tag_bind(button_rect, '<Leave>', on_leave)
        self.canvas.tag_bind(button_text, '<Enter>', on_enter)
        self.canvas.tag_bind(button_text, '<Leave>', on_leave)
    
    def handle_menu_keys(self, event):
        """Handle keyboard input in menu"""
        key = event.keysym
        print(f"Menu key pressed: {key}")  # Debug output
        
        if key == '1':
            print("Starting quick match...")
            self.start_quick_match()
        elif key == '2':
            print("Starting tournament...")
            self.start_tournament()
        elif key == '3':
            print("Starting training...")
            self.start_training()
        elif key == '4':
            print("Opening settings...")
            self.show_settings()
        elif key == '5':
            print("Exiting game...")
            self.exit_game()
        elif key == 'Escape':
            self.exit_game()
    
    def start_quick_match(self):
        """Start a quick match against AI"""
        # Show difficulty selection
        self.show_difficulty_selection()
    
    def show_difficulty_selection(self):
        """Show AI difficulty selection"""
        self.canvas.delete("all")
        self.renderer.draw_background()
        
        self.canvas.create_text(
            WINDOW_WIDTH // 2, 150,
            text="Select AI Difficulty",
            fill="yellow", font=("Arial", 20, "bold")
        )
        
        # Create clickable difficulty buttons
        difficulties = [
            ("1. Easy - Beginner friendly", PlayerType.AI_EASY),
            ("2. Medium - Balanced challenge", PlayerType.AI_MEDIUM), 
            ("3. Hard - Skilled opponent", PlayerType.AI_HARD),
            ("4. Expert - Master level", PlayerType.AI_EXPERT)
        ]
        
        for i, (text, difficulty) in enumerate(difficulties):
            button_y = 250 + i * 60
            self.create_difficulty_button(text, button_y, difficulty)
        
        # Back button
        self.create_difficulty_button("ESC. Back to Main Menu", 250 + 4 * 60, None)
        
        # Instructions
        self.canvas.create_text(
            WINDOW_WIDTH // 2, 600,
            text="Click on difficulty or press number keys",
            fill="lightgray", font=("Arial", 12)
        )
        
        # Rebind keys for difficulty selection
        self.root.unbind('<KeyPress>')
        self.root.bind('<KeyPress>', self.handle_difficulty_keys)
        self.root.focus_set()
    
    def create_difficulty_button(self, text: str, y_pos: int, difficulty):
        """Create a clickable difficulty button"""
        button_width = 500
        button_height = 40
        button_x = WINDOW_WIDTH // 2 - button_width // 2
        
        # Button background
        button_rect = self.canvas.create_rectangle(
            button_x, y_pos - button_height // 2,
            button_x + button_width, y_pos + button_height // 2,
            fill="darkgreen", outline="white", width=2
        )
        
        # Button text
        button_text = self.canvas.create_text(
            WINDOW_WIDTH // 2, y_pos,
            text=text, fill="white",
            font=("Arial", 14, "bold")
        )
        
        # Click handlers
        if difficulty is None:  # Back button
            self.canvas.tag_bind(button_rect, '<Button-1>', lambda e: self.show_main_menu())
            self.canvas.tag_bind(button_text, '<Button-1>', lambda e: self.show_main_menu())
        else:
            self.canvas.tag_bind(button_rect, '<Button-1>', lambda e: self.initialize_quick_match(difficulty))
            self.canvas.tag_bind(button_text, '<Button-1>', lambda e: self.initialize_quick_match(difficulty))
        
        # Hover effects
        def on_enter(event):
            self.canvas.itemconfig(button_rect, fill="green")
            self.canvas.itemconfig(button_text, fill="yellow")
        
        def on_leave(event):
            self.canvas.itemconfig(button_rect, fill="darkgreen")
            self.canvas.itemconfig(button_text, fill="white")
        
        self.canvas.tag_bind(button_rect, '<Enter>', on_enter)
        self.canvas.tag_bind(button_rect, '<Leave>', on_leave)
        self.canvas.tag_bind(button_text, '<Enter>', on_enter)
        self.canvas.tag_bind(button_text, '<Leave>', on_leave)
    
    def handle_difficulty_keys(self, event):
        """Handle keyboard input in difficulty selection"""
        key = event.keysym
        print(f"Difficulty key pressed: {key}")  # Debug output
        
        difficulty_map = {
            '1': PlayerType.AI_EASY, 
            '2': PlayerType.AI_MEDIUM,
            '3': PlayerType.AI_HARD, 
            '4': PlayerType.AI_EXPERT
        }
        
        if key in difficulty_map:
            print(f"Initializing match with {difficulty_map[key]}")
            self.initialize_quick_match(difficulty_map[key])
        elif key == 'Escape':
            print("Returning to main menu")
            self.show_main_menu()
    
    def initialize_quick_match(self, ai_difficulty: PlayerType):
        """Initialize quick match with selected difficulty"""
        print(f"Initializing match with difficulty: {ai_difficulty}")
        
        player_name = "Human Player"
        ai_name = f"AI {ai_difficulty.value.replace('ai_', '').title()}"
        
        # Initialize the match
        self.game_logic.initialize_match(player_name, PlayerType.HUMAN, ai_name, ai_difficulty)
        
        # Set up game controls
        self.setup_game_controls()
        
        # Start the game
        print("Starting game loop...")
        self.start_game_loop()
    
    def setup_game_controls(self):
        """Setup controls for gameplay"""
        # Unbind menu controls
        self.root.unbind('<KeyPress>')
        self.root.unbind('<KeyRelease>')
        
        # Bind game controls
        self.root.bind('<KeyPress>', self.on_key_press)
        self.root.bind('<KeyRelease>', self.on_key_release)
        
        # Mouse handling
        self.canvas.bind('<Button-1>', self.on_mouse_click)
        self.canvas.bind('<Motion>', self.on_mouse_move)
        
        # Ensure focus
        self.root.focus_set()
        print("Game controls setup complete")
    
    def start_tournament(self):
        """Start tournament mode"""
        messagebox.showinfo("Tournament", "Tournament mode coming soon!")
        self.show_main_menu()
    
    def start_training(self):
        """Start training mode"""
        print("Starting training mode...")
        self.game_logic.initialize_match("Player", PlayerType.HUMAN, "Training Bot", PlayerType.AI_EASY)
        self.setup_game_controls()
        self.start_game_loop()
    
    def show_settings(self):
        """Show settings menu"""
        settings_window = tk.Toplevel(self.root)
        settings_window.title("Settings")
        settings_window.geometry("400x300")
        settings_window.configure(bg="black")
        
        # Sound settings
        tk.Label(settings_window, text="Sound Settings", fg="white", bg="black", 
                font=("Arial", 14, "bold")).pack(pady=10)
        
        sound_frame = tk.Frame(settings_window, bg="black")
        sound_frame.pack(pady=10)
        
        tk.Checkbutton(sound_frame, text="Enable Sound Effects", 
                      variable=tk.BooleanVar(value=self.sound_manager.enabled),
                      fg="white", bg="black", selectcolor="gray").pack()
        
        # Graphics settings
        tk.Label(settings_window, text="Graphics Settings", fg="white", bg="black",
                font=("Arial", 14, "bold")).pack(pady=10)
        
        graphics_frame = tk.Frame(settings_window, bg="black") 
        graphics_frame.pack(pady=10)
        
        tk.Checkbutton(graphics_frame, text="Show Trails",
                      variable=tk.BooleanVar(value=self.renderer.show_trails),
                      fg="white", bg="black", selectcolor="gray").pack()
        
        tk.Checkbutton(graphics_frame, text="Show Statistics",
                      variable=tk.BooleanVar(value=self.renderer.show_stats),
                      fg="white", bg="black", selectcolor="gray").pack()
        
        tk.Checkbutton(graphics_frame, text="Render Particles",
                      variable=tk.BooleanVar(value=self.renderer.render_particles),
                      fg="white", bg="black", selectcolor="gray").pack()
        
        # Controls help
        tk.Label(settings_window, text="Controls", fg="white", bg="black",
                font=("Arial", 14, "bold")).pack(pady=10)
        
        controls_text = """
        WASD: Move Player
        SPACE: Charge/Release Shot
        1-6: Select Shot Type
        P: Pause Game
        R: Reset Game
        C: Cycle Camera
        T: Toggle Trails
        H: Toggle HUD
        ESC: Main Menu
        """
        
        tk.Label(settings_window, text=controls_text, fg="lightgray", bg="black",
                font=("Arial", 10), justify="left").pack(pady=10)
        
        tk.Button(settings_window, text="Close", command=settings_window.destroy,
                 bg="gray", fg="white").pack(pady=20)
    
    def start_game_loop(self):
        """Start the main game loop"""
        self.is_running = True
        self.last_update_time = time.time()
        self.game_loop()
    
    def game_loop(self):
        """Main game loop"""
        if not self.is_running:
            return
        
        current_time = time.time()
        dt = min(0.033, current_time - self.last_update_time)  # Cap at ~30 FPS for stability
        self.last_update_time = current_time
        
        # Handle input
        self.handle_movement_input(dt)
        
        # Update game logic
        self.game_logic.update(dt)
        
        # Update particle system
        self.particle_system.update(dt)
        
        # Render everything
        self.render_game()
        
        # Schedule next frame
        if self.is_running:
            self.root.after(16, self.game_loop)  # ~60 FPS
    
    def render_game(self):
        """Render the complete game"""
        # Clear screen with effects
        self.renderer.clear_screen()
        
        # Draw background
        self.renderer.draw_background()
        
        # Draw court
        self.renderer.draw_court_detailed(self.game_logic.court)
        
        # Draw players
        if self.game_logic.player1:
            self.renderer.draw_player_detailed(self.game_logic.player1, "blue")
        
        if self.game_logic.player2:
            self.renderer.draw_player_detailed(self.game_logic.player2, "red")
        
        # Draw shuttlecock
        if self.game_logic.shuttlecock:
            self.renderer.draw_shuttlecock_detailed(self.game_logic.shuttlecock, self.particle_system)
        
        # Draw UI overlay
        self.renderer.draw_ui_overlay(self.game_logic)
        
        # Draw game state specific elements
        self.draw_game_state_elements()
        
        # Update camera
        if self.game_logic.shuttlecock:
            self.renderer.update_camera(self.game_logic.shuttlecock.position)
    
    def draw_game_state_elements(self):
        """Draw elements specific to current game state"""
        state = self.game_logic.game_state
        
        if state == GameState.SERVING:
            # Draw serving indicator
            serving_player = self.game_logic.serving_player
            self.canvas.create_text(
                WINDOW_WIDTH // 2, 150,
                text=f"{serving_player.stats.name} to serve",
                fill="yellow", font=("Arial", 16, "bold")
            )
            
            if serving_player.player_type == PlayerType.HUMAN:
                self.canvas.create_text(
                    WINDOW_WIDTH // 2, 170,
                    text="Press SPACE to serve",
                    fill="lightgreen", font=("Arial", 12)
                )
        
        elif state == GameState.RALLY:
            # Draw rally information
            if self.game_logic.rally_count > 5:
                rally_text = f"Rally {self.game_logic.rally_count}"
                color = "orange" if self.game_logic.rally_count > 15 else "yellow"
                
                self.canvas.create_text(
                    WINDOW_WIDTH // 2, 120,
                    text=rally_text, fill=color,
                    font=("Arial", 14, "bold")
                )
        
        elif state == GameState.PAUSED:
            # Draw pause overlay
            self.canvas.create_rectangle(0, 0, WINDOW_WIDTH, WINDOW_HEIGHT,
                                       fill="black", stipple="gray50")
            
            self.canvas.create_text(
                WINDOW_WIDTH // 2, WINDOW_HEIGHT // 2,
                text="PAUSED", fill="white",
                font=("Arial", 32, "bold")
            )
            
            self.canvas.create_text(
                WINDOW_WIDTH // 2, WINDOW_HEIGHT // 2 + 50,
                text="Press P to resume", fill="lightgray",
                font=("Arial", 16)
            )
        
        elif state == GameState.MATCH_WON:
            # Draw victory screen
            winner = None
            if self.game_logic.sets_won[0] > self.game_logic.sets_won[1]:
                winner = self.game_logic.player1
            else:
                winner = self.game_logic.player2
            
            if winner:
                self.canvas.create_rectangle(100, 200, WINDOW_WIDTH-100, 500,
                                           fill="gold", outline="black", width=3)
                
                self.canvas.create_text(
                    WINDOW_WIDTH // 2, 280,
                    text="🏆 VICTORY! 🏆", fill="black",
                    font=("Arial", 24, "bold")
                )
                
                self.canvas.create_text(
                    WINDOW_WIDTH // 2, 320,
                    text=f"{winner.stats.name} wins!",
                    fill="black", font=("Arial", 18, "bold")
                )
                
                final_score = f"Final Score: {self.game_logic.sets_won[0]}-{self.game_logic.sets_won[1]}"
                self.canvas.create_text(
                    WINDOW_WIDTH // 2, 360,
                    text=final_score, fill="black",
                    font=("Arial", 14)
                )
                
                self.canvas.create_text(
                    WINDOW_WIDTH // 2, 420,
                    text="Press R to play again or ESC for menu",
                    fill="black", font=("Arial", 12)
                )
    
    def toggle_pause(self):
        """Toggle game pause"""
        if self.game_logic.game_state == GameState.PAUSED:
            self.game_logic.resume_game()
            if not self.is_running:
                self.start_game_loop()
        elif self.game_logic.game_state in [GameState.RALLY, GameState.SERVING]:
            self.game_logic.pause_game()
    
    def reset_game(self):
        """Reset current game"""
        if self.game_logic.player1 and self.game_logic.player2:
            self.game_logic.reset_game()
            if not self.is_running:
                self.start_game_loop()
    
    def cycle_camera(self):
        """Cycle through different camera angles"""
        # Cycle through different camera positions
        camera_positions = [
            Vector3D(COURT_WIDTH // 2, -100, 200),  # Default
            Vector3D(COURT_WIDTH // 2, COURT_HEIGHT + 100, 200),  # Opposite side
            Vector3D(-100, COURT_HEIGHT // 2, 150),  # Side view 1
            Vector3D(COURT_WIDTH + 100, COURT_HEIGHT // 2, 150),  # Side view 2
            Vector3D(COURT_WIDTH // 2, COURT_HEIGHT // 2, 300),  # Top down
        ]
        
        current_pos = self.renderer.camera_position
        
        # Find next position
        for i, pos in enumerate(camera_positions):
            if (abs(pos.x - current_pos.x) < 50 and 
                abs(pos.y - current_pos.y) < 50 and
                abs(pos.z - current_pos.z) < 50):
                next_index = (i + 1) % len(camera_positions)
                self.renderer.camera_position = camera_positions[next_index]
                return
        
        # Default to first position
        self.renderer.camera_position = camera_positions[0]
    
    def exit_game(self):
        """Exit the game"""
        self.is_running = False
        self.root.quit()
        self.root.destroy()
    
    def run(self):
        """Run the game"""
        try:
            self.root.mainloop()
        except KeyboardInterrupt:
            self.exit_game()
        except Exception as e:
            print(f"Game error: {e}")
            messagebox.showerror("Error", f"Game encountered an error: {e}")
            self.exit_game()

# Additional utility classes and functions

class CommentarySystem:
    """Provides dynamic commentary for the game"""
    
    def __init__(self):
        self.last_commentary_time = 0
        self.commentary_cooldown = 3.0
        
        self.shot_comments = {
            ShotType.SMASH: [
                "What a powerful smash!",
                "Incredible power in that shot!",
                "A devastating smash down the line!"
            ],
            ShotType.DROP: [
                "Beautiful drop shot!",
                "Perfectly placed at the net!",
                "What finesse in that drop!"
            ],
            ShotType.CLEAR: [
                "High and deep!",
                "Great defensive clear!",
                "Pushing the opponent back!"
            ],
            ShotType.DRIVE: [
                "Fast and flat!",
                "Excellent drive shot!",
                "No time to react to that one!"
            ]
        }
        
        self.rally_comments = [
            "What a rally this is turning into!",
            "Both players showing incredible skill!",
            "The shuttlecock is flying back and forth!",
            "This is badminton at its finest!",
            "Neither player wants to give up this point!"
        ]
        
        self.score_comments = [
            "And that's a point!",
            "Excellent play!",
            "The crowd goes wild!",
            "What a way to win the point!"
        ]
    
    def get_shot_commentary(self, shot_type: ShotType, is_successful: bool) -> str:
        if not is_successful:
            return random.choice([
                "Oh, that shot didn't go as planned!",
                "A rare mistake there!",
                "The shuttlecock finds the net!",
                "That one got away from them!"
            ])
        
        return random.choice(self.shot_comments.get(shot_type, ["Nice shot!"]))
    
    def get_rally_commentary(self, rally_count: int) -> str:
        if rally_count > 20:
            return "This rally is going into the record books!"
        elif rally_count > 15:
            return "What an epic rally this has become!"
        elif rally_count > 10:
            return random.choice(self.rally_comments)
        
        return ""
    
    def should_comment(self) -> bool:
        current_time = time.time()
        if current_time - self.last_commentary_time >= self.commentary_cooldown:
            self.last_commentary_time = current_time
            return True
        return False

class TournamentManager:
    """Manages tournament brackets and progression"""
    
    def __init__(self):
        self.players = []
        self.brackets = []
        self.current_round = 0
        self.tournament_name = ""
    
    def create_tournament(self, tournament_name: str, players: List[str]):
        self.tournament_name = tournament_name
        self.players = players
        self.generate_brackets()
    
    def generate_brackets(self):
        """Generate tournament brackets"""
        # Simple single elimination for now
        random.shuffle(self.players)
        
        # Pair up players
        current_round_players = self.players[:]
        round_num = 1
        
        while len(current_round_players) > 1:
            round_matches = []
            
            for i in range(0, len(current_round_players), 2):
                if i + 1 < len(current_round_players):
                    match = {
                        'player1': current_round_players[i],
                        'player2': current_round_players[i + 1],
                        'winner': None,
                        'round': round_num
                    }
                    round_matches.append(match)
                else:
                    # Bye round
                    round_matches.append({
                        'player1': current_round_players[i],
                        'player2': None,
                        'winner': current_round_players[i],
                        'round': round_num
                    })
            
            self.brackets.append(round_matches)
            current_round_players = [match['player1'] for match in round_matches if match['player2'] is None]
            round_num += 1
    
    def get_next_match(self):
        """Get the next match to be played"""
        for round_matches in self.brackets:
            for match in round_matches:
                if match['winner'] is None and match['player2'] is not None:
                    return match
        return None
    
    def record_match_result(self, match: dict, winner: str):
        """Record the result of a match"""
        match['winner'] = winner
        
        # Update next round if this round is complete
        self.update_tournament_progression()
    
    def update_tournament_progression(self):
        """Update tournament progression after match results"""
        # Check if current round is complete and advance winners
        pass

class StatisticsTracker:
    """Tracks detailed game statistics"""
    
    def __init__(self):
        self.match_stats = {}
        self.player_career_stats = {}
        self.global_stats = {
            'total_matches': 0,
            'total_rallies': 0,
            'longest_rally_ever': 0,
            'fastest_smash': 0,
            'total_playtime': 0
        }
    
    def record_match_stats(self, match_stats: MatchStats, player1: Player, player2: Player):
        """Record statistics from a completed match"""
        match_id = f"{player1.stats.name}_vs_{player2.stats.name}_{int(time.time())}"
        
        self.match_stats[match_id] = {
            'duration': match_stats.duration,
            'total_rallies': match_stats.total_rallies,
            'longest_rally': match_stats.longest_rally,
            'player1_stats': self.extract_player_stats(player1),
            'player2_stats': self.extract_player_stats(player2),
            'timestamp': time.time()
        }
        
        # Update career stats
        self.update_career_stats(player1)
        self.update_career_stats(player2)
        
        # Update global stats
        self.global_stats['total_matches'] += 1
        self.global_stats['total_rallies'] += match_stats.total_rallies
        self.global_stats['longest_rally_ever'] = max(
            self.global_stats['longest_rally_ever'], 
            match_stats.longest_rally
        )
        self.global_stats['total_playtime'] += match_stats.duration
    
    def extract_player_stats(self, player: Player) -> dict:
        """Extract relevant statistics from player"""
        return {
            'total_shots': player.stats.total_shots,
            'successful_shots': player.stats.successful_shots,
            'total_smashes': player.stats.total_smashes,
            'successful_smashes': player.stats.successful_smashes,
            'points_scored': player.stats.points_scored,
            'unforced_errors': player.stats.unforced_errors,
            'aces': player.stats.aces,
            'final_stamina': player.stats.stamina
        }
    
    def update_career_stats(self, player: Player):
        """Update career statistics for a player"""
        name = player.stats.name
        
        if name not in self.player_career_stats:
            self.player_career_stats[name] = {
                'matches_played': 0,
                'wins': 0,
                'losses': 0,
                'total_points': 0,
                'total_shots': 0,
                'total_smashes': 0,
                'best_match_duration': float('inf'),
                'average_stamina': []
            }
        
        career = self.player_career_stats[name]
        career['matches_played'] += 1
        career['wins'] += player.stats.wins
        career['losses'] += player.stats.losses
        career['total_points'] += player.stats.points_scored
        career['total_shots'] += player.stats.total_shots
        career['total_smashes'] += player.stats.total_smashes
        career['average_stamina'].append(player.stats.stamina)
        
        # Keep only recent stamina records
        if len(career['average_stamina']) > 10:
            career['average_stamina'].pop(0)
    
    def get_player_career_summary(self, player_name: str) -> dict:
        """Get career summary for a player"""
        if player_name not in self.player_career_stats:
            return {}
        
        career = self.player_career_stats[player_name]
        
        win_rate = career['wins'] / max(1, career['matches_played'])
        avg_stamina = sum(career['average_stamina']) / max(1, len(career['average_stamina']))
        
        return {
            'matches_played': career['matches_played'],
            'wins': career['wins'],
            'losses': career['losses'],
            'win_rate': win_rate,
            'total_points': career['total_points'],
            'average_stamina': avg_stamina,
            'shots_per_match': career['total_shots'] / max(1, career['matches_played'])
        }

# Game configuration and constants
class GameConfig:
    """Game configuration and settings"""
    
    # Physics settings
    GRAVITY_STRENGTH = 200
    AIR_RESISTANCE = 0.98
    GROUND_BOUNCE = 0.6
    
    # Gameplay settings
    DEFAULT_MATCH_SETS = 3
    POINTS_TO_WIN_SET = 21
    MIN_POINT_DIFFERENCE = 2
    
    # AI difficulty scaling
    AI_REACTION_TIMES = {
        'easy': 0.8,
        'medium': 0.5,
        'hard': 0.3,
        'expert': 0.1
    }
    
    # Visual settings
    TRAIL_LENGTH = 15
    PARTICLE_COUNT = 50
    SHADOW_QUALITY = 'high'
    
    @classmethod
    def load_from_file(cls, filename: str):
        """Load configuration from file"""
        try:
            with open(filename, 'r') as f:
                config_data = json.load(f)
            
            for key, value in config_data.items():
                if hasattr(cls, key.upper()):
                    setattr(cls, key.upper(), value)
        
        except FileNotFoundError:
            print(f"Config file {filename} not found, using defaults")
        except json.JSONDecodeError:
            print(f"Invalid config file {filename}, using defaults")
    
    @classmethod
    def save_to_file(cls, filename: str):
        """Save configuration to file"""
        config_data = {
            key.lower(): value for key, value in cls.__dict__.items()
            if not key.startswith('_') and isinstance(value, (int, float, str, bool, list, dict))
        }
        
        try:
            with open(filename, 'w') as f:
                json.dump(config_data, f, indent=2)
        except Exception as e:
            print(f"Failed to save config: {e}")

# Main execution
if __name__ == "__main__":
    print("🏸 Starting 3D Badminton Championship...")
    print("Loading game systems...")
    
    # Load configuration
    GameConfig.load_from_file("badminton_config.json")
    
    # Create and run game
    game = BadmintonGame()
    
    print("✅ Game initialized successfully!")
    print("🎮 Use the menu to start playing!")
    print("\n" + "="*50)
    print("CONTROLS:")
    print("WASD - Move player")
    print("SPACE - Charge/Release shot")
    print("1-6 - Select shot type")
    print("P - Pause, R - Reset, C - Camera")
    print("ESC - Main menu")
    print("="*50)
    
    try:
        game.run()
    except KeyboardInterrupt:
        print("\n🛑 Game interrupted by user")
    except Exception as e:
        print(f"\n❌ Game crashed: {e}")
        import traceback
        traceback.print_exc()
    finally:
        print("👋 Thanks for playing 3D Badminton Championship!")
        
        # Save configuration on exit
        GameConfig.save_to_file("badminton_config.json")
